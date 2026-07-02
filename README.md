# LinkedHashMap
import java.util.ArrayList;
import java.util.LinkedHashMap;
class Graph{
    ArrayList<ArrayList<Integer>>adjMat;
    LinkedHashMap<String,Integer>VertexToIndex;
    public Graph(){
        adjMat = new ArrayList<>();
        VertexToIndex = new LinkedHashMap<>();
    }
    public void addVertex(String vertex){
        if(!VertexToIndex.containsKey(vertex)){
            VertexToIndex.put(vertex,adjMat.size());
            for(ArrayList<Integer>row:adjMat){
                row.add(0);
            }
            ArrayList<Integer>newRow =new ArrayList<>();
            for(int ind = 0; ind <= adjMat.size();ind++)
            newRow.add(0);
            adjMat.add(newRow);
        }
    }
}
public class Main{
    public static void main(String[] args){
        Graph graph = new Graph();
        graph.addVertex("Anvith");
        graph.addVertex("Riyansh");
        System.out.println(graph.VertexToIndex);
        for(ArrayList<Integer>row:graph.adjMat){
            System.out.println(row);
        }
    }
        
}

    
