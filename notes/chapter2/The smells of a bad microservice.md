A bad microservice too coarse-grained will show these signs:

1. A service has too many responsibilities
2. The service is managing data across a large number of tables - Rule of thumb is 3-5 tables
3. Too many test cases

A too fine-grained one will have:

1. If we have to involve too many services to get a piece of business work done, that means the microservices are breeding like rabbits
2. Microservices heavily independent on one another
3. Microservices become an expression of business logic and not an abstraction layer over the data sources - The business logic is not reusable

```java
// Business logic is trapped in this microservice
@RestController
@RequestMapping("/orders")
public class OrderController {
    @Autowired
    private OrderRepository orderRepository;
    
    @PostMapping("/process")
    public OrderResponse processOrder(@RequestBody OrderRequest request) {
        // Direct business logic implementation
        Order order = new Order();
        order.setCustomerId(request.getCustomerId());
        order.setItems(request.getItems());
        order.setStatus("PROCESSING");
        
        // Calculate totals
        double total = request.getItems().stream()
            .mapToDouble(item -> item.getPrice() * item.getQuantity())
            .sum();
        order.setTotal(total);
        
        // Direct database operation
        orderRepository.save(order);
        
        // More business logic
        sendOrderConfirmation(order);
        updateInventory(order);
        
        return new OrderResponse(order.getId(), "Order is processing");
    }
}

// FIX: Service as Abstraction Layer
@RestController
@RequestMapping("/orders")
public class OrderController {
    @Autowired
    private OrderService orderService;
    
    @PostMapping
    public OrderResponse createOrder(@RequestBody OrderRequest request) {
        // High-level operation with minimal exposed implementation details
        return orderService.createOrder(request);
    }
    
    @GetMapping("/{id}")
    public OrderDetails getOrder(@PathVariable String id) {
        return orderService.getOrderById(id);
    }
    
    @PatchMapping("/{id}/status")
    public OrderResponse updateOrderStatus(
            @PathVariable String id, 
            @RequestBody StatusUpdateRequest request) {
        return orderService.updateStatus(id, request.getStatus());
    }
}

@Service
public class OrderService {
    @Autowired private OrderRepository orderRepository;
    @Autowired private ProductService productService;
    @Autowired private InventoryService inventoryService;
    @Autowired private NotificationService notificationService;
    
    @Transactional
    public OrderResponse createOrder(OrderRequest request) {
        // Reusable business logic hidden from API consumers
        OrderEntity order = buildInitialOrder(request);
        
        // Validate availability
        validateInventory(order);
        
        // Apply business rules
        applyPricingRules(order);
        applyDiscounts(order);
        
        // Persist
        OrderEntity savedOrder = orderRepository.save(order);
        
        // Side effects
        inventoryService.reserveItems(buildReservationRequest(order));
        notificationService.sendOrderCreationNotice(savedOrder);
        
        return new OrderResponse(savedOrder.getId(), savedOrder.getStatus());
    }
    
    // Other methods...
}
```