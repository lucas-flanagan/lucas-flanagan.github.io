---
layout: default
---

## Binary Tree Traversal

Author: Lucas Flanagan, lucasflanagan.is@gmail.com <br>
Date: 11/12/2020 <br>
Description: <br>
This is the java implementation of the binary tree described in a common coding exercise.
Search method technique: Traverse through the tree while adding nodes to a temporary queue, then remove nodes and exit if a node is located that has a name matching the keyword.

The Tree:

<img src="/images/binarytree.png">

The Code:

    import java.util.*;

    public class BinaryTree {

        // Node Class
        static class Node {

            public String name;

            Vector<Node> children = new Vector<>();

            // getName() returns name of current Node
            public String getName() {
                return this.name;
            }

            // setName() allows assignment of new name value to node
            public void setName(String newName) {
                this.name = newName;
            }

            // getChildren() returns node(s) that are the children of the referenced node.
            public Node getChildren() {
                if (this.children.size() == 1) {
                    return this.children.get(0);
                } else if (this.children.size() == 1) {
                    return this.children.get(1);
                } else {
                    return this.children.get(0);
                }
            }

            // setChildren() allows assignment of new Vector<Node> children to referenced node
            public void setChildren(Vector<Node> newChildren) {
                this.children = newChildren;
            }

        } // Node

        // Creates new node with name String
        static Node createNode(String name) {
            Node temp = new Node();
            temp.name = name;
            return temp;
        } // createNode

        // traverses through the tree starting with the root and searching for String targetName
        public static void traversalSearch(Node root, String targetName) {
            if (root == null) {
                return;
            }

            // Create a temporary queue to store nodes while traversing
            Queue<Node> myQueue = new LinkedList<>();
            myQueue.add(root);

            // While there are nodes in the queue
            while (!myQueue.isEmpty()) {
                int sizeControl = myQueue.size();

                while(sizeControl > 0) {
                    // Look at the queued node's name
                    Node peeked = myQueue.peek();
                    System.out.println(peeked.getName());

                    //print information if targetName is found, then exit the method.
                    if (peeked.getName() == targetName) {
                        System.out.println("Name Found: " + peeked.getName() + " at memory location: " + peeked);
                        return;
                    }
                    // Remove node from queue if name is not == targetName
                    myQueue.remove();

                    // Add all children of referenced node to the temp queue
                    for (int i = 0; i < peeked.children.size(); i++) {
                        myQueue.add(peeked.children.get(i));
                        sizeControl--;
                    }
                }
            }
        } // traversalSearch

        public static void main(String[] args) {

            // Creating the tree based on given diagram
            Node root = createNode("Start");
            (root.children).add(createNode("A1"));
            (root.children).add(createNode("A2"));
            (root.children.get(0).children).add(createNode("D1"));
            (root.children.get(0).children.get(0).children).add(createNode("E1"));
            (root.children.get(1).children).add(createNode("B1"));
            (root.children.get(1).children.get(0).children).add(createNode("Find Me"));
            (root.children.get(1).children).add(createNode("B2"));
            (root.children.get(1).children.get(1).children).add(createNode("C1"));

            // Calling traversalSearch method
            System.out.println("Beginning Traversal" );
            traversalSearch(root, "Find Me");

        } //Main

    } //BinaryTree

The Output:

<img src="/images/binarytreeoutput.png">
