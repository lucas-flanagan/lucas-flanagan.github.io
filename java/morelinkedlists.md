---
layout: default
---

## Linked List Manipulation

Author: Lucas Flanagan <br>
Date: 10/16/2020 <br>
Description: <br>
This is the java implementation of the linked list data structure. Contains many methods for linked list manipulation (contains(), size(), remove(), add(), set(), get(), etc.)


      package CodeHW2;

      public class CS2LinkedList<Anything> {
          // the Node class is a private inner class used (only) by the LinkedList class
          private class Node {
              private Anything data;
              private Node next;

              public Node(Anything a, Node n) {
                  data = a;
                  next = n;
              }
          }

          private Node first;
          private Node last;


          public CS2LinkedList() {

              first = null;
          }

          public boolean isEmpty() {

              return (first == null);
          }

          public void addFirst(Anything d) {
               Node temp = first;
               first = new Node(d,temp);
          }


          public void clear() {
              first = null;
          }

          public boolean contains(Anything value) {
              for (Node curr = first; curr != null; curr = curr.next) {
                  if (value.equals(curr.data))              {
                      return true;
                  }
              }
              return false;
          }


          public String toString() {
              StringBuilder result = new StringBuilder();  //String result = "";
              for (Node curr = first; curr != null; curr = curr.next)
                  result.append(curr.data + "->");  //result = result + curr.data + "->";
              result.append("[null]");
              return result.toString();   //return result + "[null]";
          }

          // ------------------------  Methods that you have to write ------------------------

          public int size() {
              Node cycle = first;
              int counter = 0;
              while (cycle != null) {
                  counter++;
                  cycle = cycle.next;
              }
              return counter;
          }

          public boolean remove(Anything m) {
              Node cycle = first;
              if (cycle != null && cycle.data == m) {
                  first = cycle.next;
                  return true;
              }
              while (cycle != null && cycle.next.data != m) {
                  cycle = cycle.next;
              }
              if (cycle != null && cycle.next.data == m) {
                  cycle = (cycle.next).next;
                  return true;
              } else {
                  return false;
                  }
          }

          public Anything getFirst() {
              Node cycle = first;
              try {
                  return cycle.data;
              } catch (NullPointerException e) {
                  System.out.println("Error: Node did not contain a value.");
                  return null;
              }
          }

          public Anything getLast() {
               Node cycle = first;
              int i = 0;
              System.out.println(this.size());
              boolean boolCheck = this.size() == 0 || this.size() == 1;
              if (boolCheck) {
                  System.out.println("Error: Node did not contain a value.");
                  return null;
              }
              System.out.println("running");
              while (i < (this.size() - 1)){
                  cycle = cycle.next;
                  i++;
              }
              try {
                  return cycle.data;
              } catch (NullPointerException e) {
                  return null;
              }
          }

          public void add(Anything value) {
              Node cycle = last;
              try {
              last = new Node(value, last.next);
              } catch (NullPointerException e) {
                  return;
              }
          }


          public Anything set(int index, Anything newValue) {
              int lastIndex = this.size() - 1;
              Node cycle = first;
              if (index > lastIndex) {
                  System.out.println("Error: Index out of range.");
                  return null;
              }
              for (int i = 0; i < index; i++) {
                  cycle = cycle.next;
              }
              Anything oldData = cycle.data;
              cycle.data = newValue;
              return oldData;
          }


          public Anything get(int index) {
              int lastIndex = this.size() - 1;
              Node cycle = first;
              if (index > lastIndex) {
                  System.out.println("Error: Index out of range.");
                  return null;
              }
              for (int i = 0; i < index; i++) {
                  cycle = cycle.next;
              }
              return cycle.data;
          }

          public void removeAll(Anything value) {
              Node cycle = first;
              while (cycle != null && cycle.data == value) {
                  first = cycle.next;
                  cycle = first;
              }
              while (cycle != null) {
                  while (cycle != null && cycle.data != value) {
                      cycle = cycle.next;
                  }
                  if (cycle == null)
                      return;
              }
          }

          public boolean equals(Object o) {
              CS2LinkedList<Anything> list = (CS2LinkedList<Anything>)o;
              Node cycle = first;
              Node cycleO = list.first;
              int lastIndexOne = this.size() - 1;
              int lastIndexTwo = list.size() - 1;
              if (lastIndexOne != lastIndexTwo) {
                  return false;
              }

              for (int i = 0; i < lastIndexOne; i++) {
                  for (int j = 0; i < lastIndexTwo; i++) {

                      if (cycle.data == cycleO.data) {
                          j++;
                          continue;
                      } else if (cycle.data != cycleO.data) {
                          return false;
                      }
                      i++;
                  }
              }

              return true;

          }

          public CS2LinkedList<Anything> split() {
              boolean isEven;
              if (this.size() % 2 == 0) {
                  isEven = true;
              } else {
                  isEven = false;
              }
              if (this.size() <= 1) {
                  return this;
              }
              CS2LinkedList<Anything> splitList = new CS2LinkedList<Anything>();
              if (isEven) {
                  int lastIndex = this.size() - 1;
                  int halfIndex = (lastIndex / 2) - 1;
                  Node cycle = first;
                  for (int j = 0; j <= halfIndex; j++) {
                      cycle = cycle.next;
                      j++;
                  }
                  for (int i = halfIndex + 1; i != lastIndex; i++) {
                      splitList.addFirst(cycle.data);
                      cycle = cycle.next;
                  }
                  return splitList;
              } else {
                  return this;
              }
          }


          public static void main(String[] args) {

          }
      }
