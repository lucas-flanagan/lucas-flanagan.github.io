---
layout: default
---

## Linked Lists & Reversal

Author: Lucas Flanagan <br>
Date: 10/28/2020 <br>
Description: <br>
This program showcases the creation of a linked list consisting of nodes, along with various methods including reverse().  

      public class MyList
      {
          static  Node myBeginning;
          static class Node
          {
              int info;
              Node pointer;

              public Node(int a)
              {
                  info = a;
              }
          }
          public void addFirst(int d)
          {
               Node temp = myBeginning;
               myBeginning = new Node(d);
               myBeginning.pointer = temp;
          }   
          public String toString()
          {
              StringBuilder result = new StringBuilder(); 
              for (Node curr = myBeginning; curr != null; curr = curr.pointer)
                  {
                      result.append(curr.info + "->");  
                  }
              result.append("[null]");
              return result.toString();   
          }

          public MyList reverse() {
              Node cycle = myBeginning;
              Node prev = null;
              Node current = null;
              while(cycle != null) {
                  current = cycle;
                  cycle = cycle.pointer;

                  current.pointer = prev;
                  prev = current;
                  myBeginning = current;
              }

              return this;
          }

          public static void main(String[] args)
          {
              MyList list1 = new MyList();
              list1.addFirst(85); 
              list1.addFirst(15); 
              list1.addFirst(25); 
              list1.addFirst(5);
              list1.addFirst(4);
              list1.addFirst(3);

              System.out.println("Given Linked list"); 
              System.out.println(list1); 
              MyList reversedList = list1.reverse(); 
              System.out.println(""); 
              System.out.println("Reversed linked list "); 
              System.out.println(reversedList); 
          }
      }
