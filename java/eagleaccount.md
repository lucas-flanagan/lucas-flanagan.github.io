---
layout: default
---

## Basic Object-Oriented Programming

Author: Lucas Flanagan <Br>
Date: 10/10/2020 <br>
Description: <br>
This is an example of a basic class structure in Java. It showcases the creation of a class with two instances and multiple methods which allow manipulation of private variables. 

      import java.util.Date;
      import java.text.DateFormat;
      import java.text.SimpleDateFormat;

      public class EagleAccount {
          private int eagleId = 0;
          private double balance;
          private String dateCreated;
          DateFormat df = new SimpleDateFormat("dd/MM/yy");

          public EagleAccount() {
              Date dateCreated = new Date();
              this.dateCreated = df.format(dateCreated);
          }
          public EagleAccount(int eagleId, double balance) {
              this.eagleId = eagleId;
              this.balance = balance;
              Date dateCreated = new Date();
              this.dateCreated = df.format(dateCreated);
          }
          public static double getBalance(EagleAccount account) {
              return account.balance;
          }
          public static void withdraw(EagleAccount account, double remove) {
              account.balance -= remove;
          }
          public static void deposit(EagleAccount account, double add) {

              account.balance += add;
          }
          public static void main(String[] args) {
              EagleAccount John = new EagleAccount(5555, 0);
              EagleAccount Mary = new EagleAccount(3456, 1000);
              withdraw(Mary, 300);
              deposit(John, 300);
              System.out.println("John's Balance = " + getBalance(John));
              System.out.println("Mary's Balance = " + getBalance(Mary));
          }
      }
