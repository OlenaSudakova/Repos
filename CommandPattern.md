/*Hello World!*/

import java.util.ArrayList;
import java.util.List;

interface Order{
    void execute();
}

class Stock{
    private String name = "ABC";
    private int quantity = 10;

    public void buy(){
        System.out.println("Stock [Name: " + name + ", Quantity: " + quantity +"] bought ");
    }

    public void sell(){
        System.out.println("Stock [Name: " + name + ", Quantity: " + quantity +"] sold ");
    }
}

class BuyStock implements Order{
    private Stock stock;

    public BuyStock(Stock stock) {
        this.stock = stock;
    }

    @Override
    public void execute() {
        stock.buy();
    }
}

class SellStock implements Order{
    private Stock stock;

    public SellStock(Stock stock) {
        this.stock = stock;
    }

    @Override
    public void execute() {
        stock.sell();
    }
}

class Broker{
    private List<Order> orderList  = new ArrayList<Order>();

    public void takeOrder(Order order){
        orderList.add(order);
    }
    public void placeOrders(){
        for (Order order: orderList){
            order.execute();
        }
        orderList.clear();
    }
}

public class Main {

    public static void main(String[] args) {

        Stock stock = new Stock();
        BuyStock buyStock = new BuyStock(stock);
        SellStock sellStock = new SellStock(stock);

        Broker broker = new Broker();
        broker.takeOrder(buyStock);
        broker.takeOrder(sellStock);

        broker.placeOrders();

    }
}
