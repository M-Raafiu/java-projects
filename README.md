# java-projects
HOTEL MANAGEMENT SYSTEM
package Project;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
import java.util.ArrayList;
import java.util.Scanner;

class Food implements Serializable {

    int itemno;
    int quantity;
    float price;

    Food(int itemno, int quantity) {
        this.itemno = itemno;
        this.quantity = quantity;
        switch (itemno) {
            case 1:
                price = quantity * 60;
                break;
            case 2:
                price = quantity * 70;
                break;
            case 3:
                price = quantity * 80;
                break;
            case 4:
                price = quantity * 50;
                break;
        }
    }
}

class SingleRoom implements Serializable {

    String Name;
    String Contact;
    String Gender;
    ArrayList <Food> food = new ArrayList<>();

    SingleRoom() {
        this.Name = "";
    }

    SingleRoom(String Name, String Contact, String Gender) {
        this.Name = Name;
        this.Contact = Contact;
        this.Gender = Gender;
    }
}

class DoubleRoom extends SingleRoom implements Serializable {

    String Name2;
    String Contact2;
    String Gender2;

    DoubleRoom() {
        this.Name = "";
        this.Name2 = "";
    }

    public DoubleRoom(String Name, String Contact, String Gender, String Name2, String Contact2, String Gender2) {
        this.Name = Name;
        this.Contact = Contact;
        this.Gender = Gender;
        this.Name2 = Name2;
        this.Contact2 = Contact2;
        this.Gender2 = Gender2;

    }
}

class NotAvailable extends Exception {

    @Override
    public String toString() {
        return "Not Available !";
    }
}

class Holder implements Serializable {

    DoubleRoom luxury_DoubleRoom[] = new DoubleRoom[10];
    DoubleRoom deluxe_DoubleRoom[] = new DoubleRoom[20];
    SingleRoom luxury_SingleRoom[] = new SingleRoom[10];
    SingleRoom deluxe_SingleRoom[] = new SingleRoom[20];
}

class Hotel {

    static Holder Hotel_ob = new Holder();
    static Scanner sc = new Scanner(System.in);

    static void CustDetails(int i, int rn) {
        String Name, Contact, Gender;
        String Name2 = null, Contact2 = null;
        String Gender2 = "";
        System.out.println("\nEnter Customer Name: ");
        Name = sc.next();
        System.out.println("\nEnter Contact Number: ");
        Contact = sc.next();
        System.out.println("\nEnter Gender: ");
        Gender = sc.next();
        if (i < 3) {
            System.out.println("Enter Second Customer Name: ");
            Name2 = sc.next();
            System.out.println("Enter Contact Number: ");
            Contact2 = sc.next();
            System.out.println("Enter Gender: ");
            Gender2 = sc.next();
        }
        switch (i) {
            case 1:
                Hotel_ob.luxury_DoubleRoom[rn] = new DoubleRoom(Name, Contact, Gender, Name2, Contact2, Gender2);
                break;
            case 2:
                Hotel_ob.deluxe_DoubleRoom[rn] = new DoubleRoom(Name, Contact, Gender, Name2, Contact2, Gender2);
                break;
            case 3:
                Hotel_ob.luxury_SingleRoom[rn] = new SingleRoom(Name, Contact, Gender);
                break;
            case 4:
                Hotel_ob.deluxe_SingleRoom[rn] = new SingleRoom(Name, Contact, Gender);
                break;
            default:
                System.out.println("Wrong option");
                break;
        }
    }

    static void BookRoom(int i) {
        int j;
        int rn;
        System.out.println("\nChoose room number from : ");
        switch (i) {
            case 1:
                for (j = 0; j < Hotel_ob.luxury_DoubleRoom.length; j++) {
                    if (Hotel_ob.luxury_DoubleRoom[j] == null) {
                        System.out.println(j + 1 + ",");
                    }
                }
                System.out.println("\nEnter room number : ");
                try {
                    rn = sc.nextInt();
                    rn--;
                    if (Hotel_ob.luxury_DoubleRoom[rn] != null) {
                        throw new NotAvailable();
                    }
                    CustDetails(i, rn);

                } catch (Exception e) {
                    System.out.println("Invalid option: ");
                    return;
                }
                break;
            case 2:
                for (j = 0; j < Hotel_ob.deluxe_DoubleRoom.length; j++) {
                    if (Hotel_ob.deluxe_DoubleRoom[j] == null) {
                        System.out.println(j + 11 + ",");
                    }
                }
                System.out.println("\nEnter room number: ");
                try {
                    rn = sc.nextInt();
                    rn = rn - 11;
                    if (Hotel_ob.deluxe_DoubleRoom[rn] != null) {
                        throw new NotAvailable();
                    }
                    CustDetails(i, rn);
                } catch (Exception e) {
                    System.out.println("Invalid option");
                    return;
                }
                break;
            case 3:
                for (j = 0; j < Hotel_ob.luxury_SingleRoom.length; j++) {
                    if (Hotel_ob.luxury_SingleRoom[j] == null) {
                        System.out.println(j + 31 + ",");
                    }
                }
                System.out.println("\nEnter room number: ");
                try {
                    rn = sc.nextInt();
                    rn = rn - 31;
                    if (Hotel_ob.luxury_SingleRoom[rn] != null) {
                        throw new NotAvailable();
                    }
                    CustDetails(i, rn);
                } catch (Exception e) {
                    System.out.println("Invalid option");
                    return;
                }
                break;
            case 4:
                for (j = 0; j < Hotel_ob.deluxe_SingleRoom.length; j++) {
                    if (Hotel_ob.deluxe_SingleRoom[j] == null) {
                        System.out.println(j + 41 + ",");
                    }
                }
                System.out.println("\nEnter room number: ");
                try {
                    rn = sc.nextInt();
                    rn = rn - 41;
                    if (Hotel_ob.deluxe_SingleRoom[rn] != null) {
                        throw new NotAvailable();
                    }
                    CustDetails(i, rn);
                } catch (Exception e) {
                    System.out.println("Invalid option: ");
                    return;
                }
                break;
            default:
                System.out.println("Enter valid option");
                break;
        }
        System.out.println("Room Booked");
    }

    static void features(int i) {
        switch (i) {
            case 1:
                System.out.println("Number of Double Beds : 1\n AC : Yes \n Free breakfast : Yes \n Charge per day : 4000 ");
                break;
            case 2:
                System.out.println("Number of Double Beds : 1\n AC : No \n Free breakfast : Yes \n Charge per day : 3000 ");
                break;
            case 3:
                System.out.println("Number of Single Beds : 1\n AC : Yes \n Free breakfast : Yes \n Charge per day : 2200 ");
                break;
            case 4:
                System.out.println("Number of Single Beds : 1\n AC : No \n Free breakfast : Yes \n Charge per day : 1200 ");
                break;
            default:
                System.out.println("Enter valid option");
                break;
        }
    }

    static void Availability(int i) {
        int j, count = 0;
        switch (i) {
            case 1:
                for (j = 0; j < 10; j++) {
                    if (Hotel_ob.luxury_DoubleRoom[j] == null) {
                        count++;
                    }
                }
                break;
            case 2:
                for (j = 0; j < Hotel_ob.deluxe_DoubleRoom.length; j++) {
                    if (Hotel_ob.deluxe_DoubleRoom[j] == null) {
                        count++;
                    }
                }
                break;
            case 3:
                for (j = 0; j < Hotel_ob.luxury_SingleRoom.length; j++) {
                    if (Hotel_ob.luxury_SingleRoom[j] == null) {
                        count++;
                    }
                }
                break;
            case 4:
                for (j = 0; j < Hotel_ob.deluxe_SingleRoom.length; j++) {
                    if (Hotel_ob.deluxe_SingleRoom[j] == null) {
                        count++;
                    }
                }
                break;
            default:
                System.out.println("Enter valid option");
                break;
        }
        System.out.println("Number of rooms available : " + count);
    }

    static void Bill(int rn, int rtype) {
        double amount = 0;
        String list[] = {"Sandwich", "Pasta", "Noodles", "Coke"};
        System.out.println("\n*******");
        System.out.println(" Bill:-");
        System.out.println("*******");

        switch (rtype) {
            case 1:
                amount += 4000;
                System.out.println("\nRoom Charge - " + 4000);
                System.out.println("\n===============");
                System.out.println("Food Charges:- ");
                System.out.println("===============");
                System.out.println("Item   Quantity    Price");
                System.out.println("-------------------------");
                for (Food obb : Hotel_ob.luxury_DoubleRoom[rn].food) {
                    amount += obb.price;
                    String format = "%-10s%-10s%-10s%n";
                    System.out.printf(format, list[obb.itemno - 1], obb.quantity, obb.price);
                }

                break;
            case 2:
                amount += 3000;
                System.out.println("Room Charge - " + 3000);
                System.out.println("\nFood Charges:- ");
                System.out.println("===============");
                System.out.println("Item   Quantity    Price");
                System.out.println("-------------------------");
                for (Food obb : Hotel_ob.deluxe_DoubleRoom[rn].food) {
                    amount += obb.price;
                    String format = "%-10s%-10s%-10s%n";
                    System.out.printf(format, list[obb.itemno - 1], obb.quantity, obb.price);
                }
                break;
            case 3:
                amount += 2200;
                System.out.println("Room Charge - " + 2200);
                System.out.println("\nFood Charges:- ");
                System.out.println("===============");
                System.out.println("Item   Quantity    Price");
                System.out.println("-------------------------");
                for (Food obb : Hotel_ob.luxury_SingleRoom[rn].food) {
                    amount += obb.price;
                    String format = "%-10s%-10s%-10s%n";
                    System.out.printf(format, list[obb.itemno - 1], obb.quantity, obb.price);
            case 4:
                amount += 1200;
                System.out.println("Room Charge - " + 1200);
                System.out.println("\nFood Charges:- ");
                System.out.println("===============");
                System.out.println("Item   Quantity    Price");
                System.out.println("-------------------------");
                for (Food obb : Hotel_ob.deluxe_SingleRoom[rn].food) {
                    amount += obb.price;
                    String format = "%-10s%-10s%-10s%n";
                    System.out.printf(format, list[obb.itemno - 1], obb.quantity, obb.price);
                }
                break;
            default:
                System.out.println("Not valid");
        }
        System.out.println("\nTotal Amount- " + amount);
    }

    static void Deallocate(int rn, int rtype) {
        int j;
        char w;
        switch (rtype) {
            case 1:
                if (Hotel_ob.luxury_DoubleRoom[rn] != null) {
                    System.out.println("Room used by " + Hotel_ob.luxury_DoubleRoom[rn].Name);
                } else {
                    System.out.println("Empty Already");
                    return;
                }
                System.out.println("Do you want to checkout ?(y/n)");
                w = sc.next().charAt(0);
                if (w == 'y' || w == 'Y') {
                    Bill(rn, rtype);
                    Hotel_ob.luxury_DoubleRoom[rn] = null;
                    System.out.println("Deallocated succesfully");
                }

                break;
            case 2:
                if (Hotel_ob.deluxe_DoubleRoom[rn] != null) {
                    System.out.println("Room used by " + Hotel_ob.deluxe_DoubleRoom[rn].Name);
                } else {
                    System.out.println("Empty Already");
                    return;
                }
                System.out.println(" Do you want to checkout ?(y/n)");
                w = sc.next().charAt(0);
                if (w == 'y' || w == 'Y') {
                    Bill(rn, rtype);
                    Hotel_ob.deluxe_DoubleRoom[rn] = null;
                    System.out.println("Deallocated succesfully");
                }

                break;
            case 3:
                if (Hotel_ob.luxury_SingleRoom[rn] != null) {
                    System.out.println("Room used by " + Hotel_ob.luxury_SingleRoom[rn].Name);
                } else {
                    System.out.println("Empty Already");
                    return;
                }
                System.out.println(" Do you want to checkout ? (y/n)");
                w = sc.next().charAt(0);
                if (w == 'y' || w == 'Y') {
                    Bill(rn, rtype);
                    Hotel_ob.luxury_SingleRoom[rn] = null;
                    System.out.println("Deallocated succesfully");
                }

                break;
            case 4:
                if (Hotel_ob.deluxe_SingleRoom[rn] != null) {
                    System.out.println("Room used by " + Hotel_ob.deluxe_SingleRoom[rn].Name);
                } else {
                    System.out.println("Empty Already");
                    return;
                }
                System.out.println(" Do you want to checkout ? (y/n)");
                w = sc.next().charAt(0);
                if (w == 'y' || w == 'Y') {
                    Bill(rn, rtype);
                    Hotel_ob.deluxe_SingleRoom[rn] = null;
                    System.out.println("Deallocated succesfully");
                }
                break;
            default:
                System.out.println("\nEnter valid option : ");
                break;
        }
    }

    static void order(int rn, int rtype) {
        int i, q;
        char wish;
        try {
            System.out.println("\n==========\n   Menu:  \n==========\n\n1.Sandwich\tRs.60\n2.Pasta\t\tRs.70\n3.Noodles\tRs.80\n4.Coke\t\tRs.50\n");
            do {
                i = sc.nextInt();
                System.out.print("Quantity- ");
                q = sc.nextInt();

                switch (rtype) {
                    case 1:
                        Hotel_ob.luxury_DoubleRoom[rn].food.add(new Food(i, q));
                        break;
                    case 2:
                        Hotel_ob.deluxe_DoubleRoom[rn].food.add(new Food(i, q));
                        break;
                    case 3:
                        Hotel_ob.luxury_SingleRoom[rn].food.add(new Food(i, q));
                        break;
                    case 4:
                        Hotel_ob.deluxe_SingleRoom[rn].food.add(new Food(i, q));
                        break;
                }
                System.out.println("Do you want to order anything else ? (y/n)");
                wish = sc.next().charAt(0);
            } while (wish == 'y' || wish == 'Y');
        } catch (NullPointerException e) {
            System.out.println("\nRoom not booked");
        } catch (Exception e) {
            System.out.println("Cannot be done");
        }
    }
}

class write implements Runnable {

    Holder Hotel_ob;

    write(Holder Hotel_ob) {
        this.Hotel_ob = Hotel_ob;
    }

    @Override
    public void run() {
        try {
            FileOutputStream fout = new FileOutputStream("backup");
            ObjectOutputStream oos = new ObjectOutputStream(fout);
            oos.writeObject(Hotel_ob);
        } catch (Exception e) {
            System.out.println("Error in writing " + e);
        }

    }

}

public class Main {

    public static void main(String[] args) {

        try {
            File f = new File("backup");
            if (f.exists()) {
                FileInputStream fin = new FileInputStream(f);
                ObjectInputStream ois = new ObjectInputStream(fin);
                Hotel.Hotel_ob = (Holder) ois.readObject();
            }
            Scanner sc = new Scanner(System.in);
            int ch, ch2;
            char wish;
            x:
            do {

                System.out.println("\nEnter your choice :\n1.Display room details\n2.Display room availability \n3.Book\n4.Order food\n5.Checkout\n6.Exit\n");
                ch = sc.nextInt();
                switch (ch) {
                    case 1:
                        System.out.println("\nChoose room type :\n1.Luxury Double Room \n2.Deluxe Double Room \n3.Luxury Single Room \n4.Deluxe Single Room\n");
                        ch2 = sc.nextInt();
                        Hotel.features(ch2);
                        break;
                    case 2:
                        System.out.println("\nChoose room type :\n1.Luxury Double Room \n2.Deluxe Double Room \n3.Luxury Single Room\n4.Deluxe Single Room\n");
                        ch2 = sc.nextInt();
                        Hotel.Availability(ch2);
                        break;
                    case 3:
                        System.out.println("\nChoose room type :\n1.Luxury Double Room \n2.Deluxe Double Room \n3.Luxury Single Room\n4.Deluxe Single Room\n");
                        ch2 = sc.nextInt();
                        Hotel.BookRoom(ch2);
                        break;
                    case 4:
                        System.out.print("Room Number -");
                        ch2 = sc.nextInt();
                        if (ch2 > 60) {
                            System.out.println("Room doesn't exist");
                        } else if (ch2 > 40) {
                            Hotel.order(ch2 - 41, 4);
                        } else if (ch2 > 30) {
                            Hotel.order(ch2 - 31, 3);
                        } else if (ch2 > 10) {
                            Hotel.order(ch2 - 11, 2);
                        } else if (ch2 > 0) {
                            Hotel.order(ch2 - 1, 1);
                        } else {
                            System.out.println("Room doesn't exist");
                        }
                        break;
                    case 5:
                        System.out.print("Room Number -");
                        ch2 = sc.nextInt();
                        if (ch2 > 60) {
                            System.out.println("Room doesn't exist");
                        } else if (ch2 > 40) {
                            Hotel.Deallocate(ch2 - 41, 4);
                        } else if (ch2 > 30) {
                            Hotel.Deallocate(ch2 - 31, 3);
                        } else if (ch2 > 10) {
                            Hotel.Deallocate(ch2 - 11, 2);
                        } else if (ch2 > 0) {
                            Hotel.Deallocate(ch2 - 1, 1);
                        } else {
                            System.out.println("Room doesn't exist");
                        }
                        break;
                    case 6:
                        break x;

                }

                System.out.println("\nContinue : (y/n)");
                wish = sc.next().charAt(0);
                if (!(wish == 'y' || wish == 'Y' || wish == 'n' || wish == 'N')) {
                    System.out.println("Invalid Option");
                    System.out.println("\nContinue : (y/n)");
                    wish = sc.next().charAt(0);
                }

            } while (wish == 'y' || wish == 'Y');

            Thread t = new Thread(new write(Hotel.Hotel_ob));
            t.start();
        } catch (Exception e) {
            System.out.println("Not a valid input");
        }
    }
}
}

                break;
 
