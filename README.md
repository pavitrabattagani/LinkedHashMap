# LinkedHashMap
import java.util.ArrayList;
import java.util.LinkedHashMap;

class Graph{
    ArrayList<ArrayList<Integer>> adjMat;
    LinkedHashMap<String, Integer> VertexToIndex;
    
    public Graph(){
        adjMat = new ArrayList<>();
        VertexToIndex = new LinkedHashMap<>();
    }
    
    private void addVertex(String vertex){
        if(!VertexToIndex.containsKey(vertex)){
            VertexToIndex.put(vertex, adjMat.size());
            for(ArrayList<Integer> row : adjMat){
                row.add(0);
            }
            ArrayList<Integer> newRow = new ArrayList<>();
            for(int ind=0; ind <= adjMat.size(); ind++)
                newRow.add(0);
            adjMat.add(newRow);
        }
    }
    
    public void addEdge(String source, String destination,int weight){
        addVertex(source);
        addVertex(destination);
        
        int row = VertexToIndex.get(source);
        int col = VertexToIndex.get(destination);
        
        adjMat.get(row).set(col,weight);
        adjMat.get(col).set(row,weight);
    }
    
    public void display(){
        for(int ind=0;ind<10;ind++)
            System.out.print(" ");
            
        for(String vertex: VertexToIndex.keySet()){
            System.out.printf("%-10s",vertex);
        }
        System.out.println();
        for(String vertex: VertexToIndex.keySet()){
            System.out.printf("%-10s",vertex);
            int row = VertexToIndex.get(vertex);
            for(int col = 0; col < adjMat.size(); col++){
                System.out.printf("%-10d",adjMat.get(row).get(col));
            }
            System.out.println();
        }
    }
}

public class Main
{
	public static void main(String[] args) {
		Graph graph = new Graph();
		graph.addEdge("Harish","Kumar",10);
		graph.display();
	}
}

    



#BFS Traversal

import java.util.ArrayList;
import java.util.LinkedHashMap;


class Graph{
    LinkedHashMap<String,ArrayList<String>> AdjList;
    
    public Graph(){
        AdjList = new LinkedHashMap<>();
    }
    
    public void addEdge(String source, String destination){
        if(!AdjList.containsKey(source)) {
            AdjList.put(source, new ArrayList<>());
        }
        
        if(!AdjList.containsKey(destination)) {
            AdjList.put(destination, new ArrayList<>());
        }
        
        AdjList.get(source).add(destination);
        AdjList.get(destination).add(source);
    }
    
    public void display(){
        for(String vertex : AdjList.keySet()){
            System.out.println(vertex +" -> "+ AdjList.get(vertex));
        }
    }
}
public class Main
{
	public static void main(String[] args) {
		Graph graph = new Graph();
		graph.addEdge("10","19");
		graph.addEdge("10","17");
		graph.addEdge("17","11");
		graph.addEdge("11","19");
		graph.addEdge("17","23");
		graph.display();
	}
}






import java.util.ArrayList;
import java.util.LinkedHashMap;
import java.util.Queue;
import java.util.LinkedList;
import java.util.HashSet;

class Graph{
    LinkedHashMap<String,ArrayList<String>> AdjList;
    
    public Graph(){
        AdjList = new LinkedHashMap<>();
    }
    
    public void addEdge(String source, String destination){
        if(!AdjList.containsKey(source)) {
            AdjList.put(source, new ArrayList<>());
        }
        
        if(!AdjList.containsKey(destination)) {
            AdjList.put(destination, new ArrayList<>());
        }
        
        AdjList.get(source).add(destination);
        AdjList.get(destination).add(source);
    }
    
    public void display(){
        for(String vertex : AdjList.keySet()){
            System.out.println(vertex +" -> "+ AdjList.get(vertex));
        }
    }
    
    public void levelOrderTraverse(String start){
        Queue<String> queue = new LinkedList<>();
        queue.offer(start);
        HashSet<String> visited = new HashSet<>();
        visited.add(start);
        while(!queue.isEmpty()){
            String currentVertex = queue.poll();
            System.out.print(currentVertex+ " ");
            for(String neighbour: AdjList.get(currentVertex)){
                if(!visited.contains(neighbour)){
                    visited.add(neighbour);
                    queue.offer(neighbour);
                }
            }
        }
    }
}
public class Main
{
	public static void main(String[] args) {
		Graph graph = new Graph();
		graph.addEdge("10","19");
		graph.addEdge("10","17");
		graph.addEdge("17","11");
		graph.addEdge("11","19");
		graph.addEdge("17","23");
		graph.levelOrderTraverse("10");
	}
}




#undirected unweighted

import java.util.ArrayList;
import java.util.LinkedHashMap;
import java.util.Queue;
import java.util.LinkedList;
import java.util.HashSet;

class Pair{
    String child, parent;
    
    public Pair(String child, String parent){
        this.child = child;
        this.parent = parent;
    }
}

class Graph{
    LinkedHashMap<String,ArrayList<String>> AdjList;
    
    public Graph(){
        AdjList = new LinkedHashMap<>();
    }
    
    public void addEdge(String source, String destination){
        if(!AdjList.containsKey(source)) {
            AdjList.put(source, new ArrayList<>());
        }
        
        if(!AdjList.containsKey(destination)) {
            AdjList.put(destination, new ArrayList<>());
        }
        
        AdjList.get(source).add(destination);
        AdjList.get(destination).add(source);
    }
    
    public void display(){
        for(String vertex : AdjList.keySet()){
            System.out.println(vertex +" -> "+ AdjList.get(vertex));
        }
    }
    
    public void levelOrderTraverse(String start){
        Queue<String> queue = new LinkedList<>();
        queue.offer(start);
        HashSet<String> visited = new HashSet<>();
        visited.add(start);
        while(!queue.isEmpty()){
            String currentVertex = queue.poll();
            System.out.print(currentVertex+ " ");
            for(String neighbour: AdjList.get(currentVertex)){
                if(!visited.contains(neighbour)){
                    visited.add(neighbour);
                    queue.offer(neighbour);
                }
            }
        }
    }
    public boolean havingCycleBfs(String start){
        Queue<Pair> queue = new LinkedList<>();
        HashSet<String> visited = new HashSet<>();
        visited.add(start);
        queue.offer(new Pair (start,"-1"));
        while(!queue.isEmpty()){
            Pair current = queue.poll();
            String child = current.child;
            String parent = current.parent;
            for(String neighbour : AdjList.get(child)){
                if(!visited.contains(neighbour)){
                    queue.offer(new Pair(neighbour,child));
                    visited.add(neighbour);
                }
                else{
                    if(!neighbour.equals(parent))
                        return true;
                }
            }
        }
        return false;
    }
}
public class Main{
	public static void main(String[] args) {
		Graph graph = new Graph();
		graph.addEdge("10","19");
		graph.addEdge("17","10");
		graph.addEdge("17","11");
		graph.addEdge("11","19");
		graph.addEdge("17","23");
		System.out.print(graph.havingCycleBfs("10"));
	}
}







