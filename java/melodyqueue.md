---
layout: default
---

## Temporary Queues/Stacks within a Class

Author: Lucas Flanagan <br>
Date: 11/01/2020 <br>
Description: <br>
This package utilizes queues and stacks in order to allow the user to load, play, and reverse inputted song files among many other functions. The MelodyQueue file provides the framework for the queue (linked-list variation) needed in order to permit use of other classes within the package.

      import java.util.*;

      public class MelodyQueue {

          private Node front;
          private Node back;
          private double duration;
          private int size;
          private double repeatDuration;

          public MelodyQueue() {
              front = null;
              back = null;
              double duration = 0;
              size = 0;
              repeatDuration = 0;

          }

          //Enqueue: Adds item to the queue
          public void enqueue(Object item) {
              Node x = new Node(item);
              if (front == null && back == null) {
                  front = x;
                  back = x;
              }
              back.setNext(x);
              back = x;
          }
          //Dequeue: Removes item from the queue; returns item from front.
          public Object dequeue() {
              // Return item from front of queue
              if (!front.hasNext()) {
                  throw new RuntimeException("Queue underflow");
              } else if (front == back) {
                  front = null;
                  back = null;
              }
              Node tempReturn = front;
              front = front.getNext();
              return tempReturn;
          }

          public Boolean isEmpty() {
              //Return true if queue is empty
              return (front == null && back == null);
          }

          public double duration() {
              //Return total length of song in sec, accounting for repeated segments
              Node temp = front;
              double runningDuration = 0;
              while (temp.hasNext()) {
                  runningDuration += ((Note)(temp.getItem())).getDuration();
                  temp = temp.getNext();
              }
              // calling external timeRepeat() method
              timeRepeat();
              if (repeatDuration != 0) {
                  runningDuration += repeatDuration;
              }
              return runningDuration;
          }

          public double timeRepeat() {
              //Cycle through nodes, summing duration of repeated elements; return total repeated duration
              Node cycle = front;
              while (cycle.getNext() != null) {
                  if(((Note)(cycle.getItem())).isRepeat() == true) {
                      double theDuration = ((Note)(cycle.getItem())).getDuration();
                      repeatDuration += theDuration;
                  }
                  cycle = cycle.getNext();
              }
              return repeatDuration;
          }

          public int size() {
              //Return size of queue
              size = 0;
              Node temp = front;
              while (temp.getNext() != null) {
                  size += 1;
                  temp = temp.getNext();
              }
              return size;
          }

          public String makeString() {
              //Returns a string containing lines of information about each note
              Node temp = front;
              String myString = "";
              while (temp.hasNext()) {
                  myString += (Double.toString((((Note)temp.getItem())).getDuration())) + " ";
                  myString += ((((Note)temp.getItem()).getPitch())) + " ";
                  myString += (Integer.toString((((Note)temp.getItem())).getOctave())) + " ";
                  myString += ((((Note)temp.getItem())).getAccidental()) + " ";
                  myString += (Boolean.toString((((Note)temp.getItem())).isRepeat())) + "\n"; // newline
                  temp = temp.getNext();
              }
              return myString;
          }

          public void tempoChange(double tempo) {
              //Changes tempo of each note to a percentage of what it previously was
              Node temp = front;
              while (temp.hasNext()) {
                  ((Note)(temp.getItem())).setDuration(((Note)(temp.getItem())).getDuration() * tempo);
                  temp = temp.getNext();
              }
          }

          public void play() {
              //plays song
              Node temp = front;
              if (front == null && back == null) { //Underflow check
                  System.out.println("Queue Underflow.");
              } else {
                  MelodyQueue repeated = new MelodyQueue();
                  while(temp.getNext() != null) {
                      // Create new temp queue for repeated segment
                      if (((Note)((temp.getNext()).getItem())).isRepeat()) {
                          boolean rpt = true;
                          while (rpt) {
                              repeated.enqueue(temp.getNext().getItem());
                              ((Note) (temp.getItem())).play();
                              temp = temp.getNext();
                              if (((Note)((temp.getNext()).getItem())).isRepeat()) {
                                  repeated.enqueue(temp.getNext());
                                  ((Note) (temp.getItem())).play();
                                  temp = temp.getNext();
                                  rpt = false;
                                  //Play repeated segment (from temp queue)
                                  repeated.playRepeat();
                              }
                          }
                      }
                      //Play remaining segment after repeat
                      ((Note) (temp.getItem())).play();
                      temp = temp.getNext();
                  }
              }
          }
          //Used to allow external reference to private front variable
          public Node getFront() {
              return front;
          }

          public void playRepeat() {
              //Plays repeated sections
              Node temp = front;
              ((Note) (temp.getItem())).play();
              temp = temp.getNext();
          }

          public void appendMelody(MelodyQueue other) {
              //adds one melody onto the end of another
              //song = this song + notes of song in parameter
              Node tempTwo = other.getFront();
              while (tempTwo.getNext() != null) {
                  this.enqueue(tempTwo.getItem());
                  tempTwo = tempTwo.getNext();
              }
          }

          public MelodyQueue reverseMelody() {
              //reverses the order of the notes in a song and returns the song
              Node temp = front;
              Stack stackGANG = new Stack();
              while(temp.hasNext()) {
                  stackGANG.push(((temp.getItem())));
                  this.dequeue();
                  Node hold = temp.getNext();
                  temp = hold;
              }
              front = null;
              back = null;
              while(!stackGANG.isEmpty()) {
                  this.enqueue(stackGANG.pop());
              }

              return this;
          }
          // main method
          public static void main(String[] args) {

          }

      }
