package machine;

import java.util.Scanner;

public class CoffeeMachine {
    private int waterHeld;
    private int milkHeld;
    private int beansHeld;
    private int cupsHeld;
    private int moneyHeld;
    private Status status;
    private Scanner scan = new Scanner(System.in);

    private CoffeeMachine() {
        this.waterHeld = 400;
        this.milkHeld = 540;
        this.beansHeld = 120;
        this.cupsHeld = 9;
        this.moneyHeld = 550;
        this.status = Status.STANDBY;
    }

    private enum Status {
        STANDBY,
        BUY,
        FILL,
        TAKE,
        DISPLAY_INFO,
        OFF
    }

    private enum CoffeeType {
        ESPRESSO (250, 0, 16, 4),
        LATTE (350, 75, 20, 7),
        CAPPUCCINO (200, 100, 12, 6);

        int waterNeeded;
        int milkNeeded;
        int beansNeeded;
        int cost;

        CoffeeType(int waterNeeded, int milkNeeded, int beansNeeded, int cost) {
            this.waterNeeded = waterNeeded;
            this.milkNeeded = milkNeeded;
            this.beansNeeded = beansNeeded;
            this.cost = cost;
        }

        public int getWaterNeeded() {
            return waterNeeded;
        }

        public int getMilkNeeded() {
            return milkNeeded;
        }

        public int getBeansNeeded() {
            return beansNeeded;
        }

        public int getCost() {
            return cost;
        }
    }

    public static void main(String[] args) {
        CoffeeMachine coffeeMachine = new CoffeeMachine();

        while(coffeeMachine.status != Status.OFF) {
            coffeeMachine.processAction();
        }

    }

    private void processAction() {
        System.out.println("Write action (buy, fill, take, remaining, exit):");

        switch (scan.nextLine().toLowerCase()) {
            case "buy":
                status = Status.BUY;
                processBuy();
                break;
            case "fill":
                status = Status.FILL;
                processFill();
                break;
            case "take":
                status = Status.TAKE;
                processTake();
                break;
            case "remaining":
                status = Status.DISPLAY_INFO;
                processDisplay();
                break;
            case "exit":
                status = Status.OFF;
                break;
            default:
                System.out.println("Invalid selection, please try again");
                status = Status.STANDBY;
        }
    }

    private void processBuy() {
        System.out.println("What do you want to buy? 1 - espresso, 2 - latte, 3 - cappuccino, back - to main menu:");

        switch (scan.nextLine()) {
            case "1":
                brew(CoffeeType.ESPRESSO);
                break;
            case "2":
                brew(CoffeeType.LATTE);
                break;
            case "3":
                brew(CoffeeType.CAPPUCCINO);
                break;
            default:
                status = Status.STANDBY;
                break;
        }
    }

    private void brew(CoffeeType coffee) {

        if (coffee.getWaterNeeded() > waterHeld) {
            System.out.println("Sorry, not enough water!");
        } else if (coffee.getMilkNeeded() > milkHeld) {
            System.out.println("Sorry, not enough milk!");
        } else if (coffee.getBeansNeeded() > beansHeld) {
            System.out.println("Sorry, not enough coffee beans!");
        } else if (1 > cupsHeld) {
            System.out.println("Sorry, not enough cups!");
        } else {
            waterHeld -= coffee.getWaterNeeded();
            milkHeld -= coffee.getMilkNeeded();
            beansHeld -= coffee.getBeansNeeded();
            cupsHeld--;
            moneyHeld += coffee.getCost();
        }

        status = Status.STANDBY;
    }

    private void processFill() {
        System.out.println("Write how many ml of water you want to add:");
        int water = scan.nextInt();
        System.out.println("Write how many ml of milk you want to add:");
        int milk = scan.nextInt();
        System.out.println("Write how many grams of coffee beans you want to add:");
        int beans = scan.nextInt();
        System.out.println("Write how many disposable cups you want to add:");
        int cups = scan.nextInt();
        fill(water, milk, beans, cups);
    }

    private void fill(int water, int milk, int beans, int cups) {
        this.waterHeld += water;
        this.milkHeld += milk;
        this.beansHeld += beans;
        this.cupsHeld += cups;

        status = Status.STANDBY;
    }

    private void processTake() {
        System.out.printf("I gave you $%d", moneyHeld);
        moneyHeld = 0;
    }

    private void processDisplay() {
        System.out.println("The coffee machine has:\n" +
                String.format("%d of water\n", waterHeld) +
                String.format("%d of milk\n", milkHeld) +
                String.format("%d of coffee beans\n", beansHeld) +
                String.format("%d of disposable cups\n", cupsHeld) +
                String.format("$%d of money", moneyHeld));

        status = Status.STANDBY;
    }
}
