### **1. Basic Topological Spaces**

1. **Determine if a Given Collection Forms a Topology**:
   - **Problem**: Given a set \( X = \{1, 2, 3\} \) and a collection \( \mathcal{T} = \{\emptyset, \{1\}, \{1, 2\}, \{1, 2, 3\}\} \), determine if \( \mathcal{T} \) is a topology on \( X \).
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <set>
     #include <vector>
     #include <unordered_set>
     
     bool isTopology(const std::unordered_set<std::set<int>>& collection, const std::set<int>& X) {
         if (collection.find(std::set<int>()) == collection.end() || collection.find(X) == collection.end()) {
             return false;
         }
         for (const auto& set1 : collection) {
             for (const auto& set2 : collection) {
                 std::set<int> intersection;
                 std::set_intersection(set1.begin(), set1.end(), set2.begin(), set2.end(), std::inserter(intersection, intersection.begin()));
                 if (set1 != set2 && collection.find(intersection) == collection.end()) {
                     return false;
                 }
             }
         }
         return true;
     }
     
     int main() {
         std::set<int> X = {1, 2, 3};
         std::unordered_set<std::set<int>> T = { {}, {1}, {1, 2}, {1, 2, 3} };
         
         if (isTopology(T, X)) {
             std::cout << "The collection forms a topology.\n";
         } else {
             std::cout << "The collection does not form a topology.\n";
         }
         return 0;
     }
     ```

2. **Find the Closure of a Set in a Given Topology**:
   - **Problem**: Given \( X = \mathbb{R} \) with the standard topology, find the closure of the set \( (0, 1) \).
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <set>
     
     std::set<int> closure(const std::set<int>& S, const std::set<std::set<int>>& T) {
         std::set<int> closed_set = S;
         std::set<int> intersection;
         for (const auto& open_set : T) {
             if (open_set.find(0) != open_set.end() && open_set.find(1) != open_set.end()) {
                 closed_set.insert(0);
                 closed_set.insert(1);
             }
         }
         return closed_set;
     }
     
     int main() {
         std::set<int> S = {0, 1}; // Example for simplicity
         std::set<std::set<int>> T = { {0, 1}, {1, 2}, {0, 2}, {0, 1, 2} };
         
         std::set<int> result = closure(S, T);
         std::cout << "Closure: ";
         for (int elem : result) {
             std::cout << elem << " ";
         }
         std::cout << std::endl;
         return 0;
     }
     ```

### **2. Simplicial Complexes**

3. **Construct the Simplicial Complex for a 2D Triangle**:
   - **Problem**: Given a 2D triangle with vertices \( A, B, C \), construct the simplicial complex.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Simplex {
         std::vector<int> vertices;
     };
     
     void printComplex(const std::vector<Simplex>& complex) {
         for (const auto& simplex : complex) {
             std::cout << "{";
             for (size_t i = 0; i < simplex.vertices.size(); ++i) {
                 std::cout << simplex.vertices[i];
                 if (i < simplex.vertices.size() - 1) {
                     std::cout << ", ";
                 }
             }
             std::cout << "}" << std::endl;
         }
     }
     
     int main() {
         std::vector<Simplex> triangleComplex = {
             {{0, 1}}, // Edge AB
             {{1, 2}}, // Edge BC
             {{2, 0}}, // Edge CA
             {{0, 1, 2}} // Face ABC
         };
         
         std::cout << "Simplicial Complex:" << std::endl;
         printComplex(triangleComplex);
         return 0;
     }
     ```

4. **Compute the 1-Skeleton of a 3D Cube**:
   - **Problem**: Construct the 1-skeleton (edges) of a 3D cube.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Edge {
         int start, end;
     };
     
     void printEdges(const std::vector<Edge>& edges) {
         for (const auto& edge : edges) {
             std::cout << "(" << edge.start << ", " << edge.end << ")" << std::endl;
         }
     }
     
     int main() {
         std::vector<Edge> cubeEdges = {
             {0, 1}, {1, 2}, {2, 3}, {3, 0},
             {4, 5}, {5, 6}, {6, 7}, {7, 4},
             {0, 4}, {1, 5}, {2, 6}, {3, 7}
         };
         
         std::cout << "Edges of the Cube:" << std::endl;
         printEdges(cubeEdges);
         return 0;
     }
     ```

### **3. Persistent Homology**

5. **Compute the Persistent Homology Barcode for a Simple Filtered Complex**:
   - **Problem**: Given a simple filtration of a 2D simplex complex, compute the barcode.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Interval {
         int birth, death;
     };
     
     void printBarcode(const std::vector<Interval>& barcode) {
         for (const auto& interval : barcode) {
             std::cout << "[" << interval.birth << ", " << interval.death << ")" << std::endl;
         }
     }
     
     int main() {
         std::vector<Interval> barcode = {
             {0, 2}, // Component appears at time 0, disappears at time 2
             {1, 3}  // Hole appears at time 1, disappears at time 3
         };
         
         std::cout << "Barcode:" << std::endl;
         printBarcode(barcode);
         return 0;
     }
     ```

6. **Construct a Persistence Diagram from a Barcode**:
   - **Problem**: Convert a barcode to a persistence diagram.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Point {
         int birth, death;
     };
     
     void printDiagram(const std::vector<Point>& diagram) {
         for (const auto& point : diagram) {
             std::cout << "(" << point.birth << ", " << point.death << ")" << std::endl;
         }
     }
     
     int main() {
         std::vector<Point> diagram = {
             {0, 2},
             {1, 3}
         };
         
         std::cout << "Persistence Diagram:" << std::endl;
         printDiagram(diagram);
         return 0;
     }
     ```

### **4. Mesh Processing**

7. **Generate a Simple Mesh from a Triangulated Surface**:
   - **Problem**: Create a simple 2D mesh from a triangulated surface.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Triangle {
         int v0, v1, v2;
     };
     
     void printMesh(const std::vector<Triangle>& mesh) {
         for (const auto& tri : mesh) {
             std::cout << "Triangle: (" << tri.v0 << ", " << tri.v1 << ", " << tri.v2 << ")" << std::endl;
         }
     }
     
     int main() {
         std::vector<Triangle> mesh = {
             {0, 1, 2},
             {2, 3, 0}
         };
         
         std::cout << "Mesh:" << std::endl;
         printMesh(mesh);
         return 0;
     }
     ```

8. **Simplify a Mesh Using Edge Collapse**:
   - **Problem**: Simplify a mesh by collapsing an edge.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Vertex {
         int id;
         double x, y;
     };
     
     struct Edge {
         int v0, v1;
     };
     
     void collapseEdge(std::vector<Vertex>& vertices, std::vector<Edge>& edges, int v0, int v1) {
         std

::vector<Edge> newEdges;
         for (const auto& edge : edges) {
             if ((edge.v0 == v0 && edge.v1 == v1) || (edge.v0 == v1 && edge.v1 == v0)) {
                 continue;
             }
             if (edge.v0 == v1) {
                 newEdges.push_back({v0, edge.v1});
             } else if (edge.v1 == v1) {
                 newEdges.push_back({edge.v0, v0});
             } else {
                 newEdges.push_back(edge);
             }
         }
         edges = newEdges;
     }
     
     int main() {
         std::vector<Vertex> vertices = {
             {0, 0.0, 0.0},
             {1, 1.0, 0.0},
             {2, 0.5, 1.0}
         };
         std::vector<Edge> edges = {
             {0, 1},
             {1, 2},
             {2, 0}
         };
         
         collapseEdge(vertices, edges, 1, 2);
         
         std::cout << "Edges after collapsing edge (1, 2):" << std::endl;
         for (const auto& edge : edges) {
             std::cout << "(" << edge.v0 << ", " << edge.v1 << ")" << std::endl;
         }
         return 0;
     }
     ```

### **5. Applications and Algorithms**

9. **Calculate the Betti Numbers for a Simple Complex**:
   - **Problem**: Compute Betti numbers for a simple simplicial complex.
   - **Solution**:
     ```cpp
     #include <iostream>
     #include <vector>
     
     struct Simplex {
         std::vector<int> vertices;
     };
     
     int calculateBettiNumber(const std::vector<Simplex>& complex, int dimension) {
         int count = 0;
         for (const auto& simplex : complex) {
             if (simplex.vertices.size() == dimension + 1) {
                 ++count;
             }
         }
         return count;
     }
     
     int main() {
         std::vector<Simplex> complex = {
             {{0}},   // 0-dimensional simplex (vertex)
             {{0, 1}}, // 1-dimensional simplex (edge)
             {{0, 1, 2}} // 2-dimensional simplex (face)
         };
         
         int betti0 = calculateBettiNumber(complex, 0);
         int betti1 = calculateBettiNumber(complex, 1);
         int betti2 = calculateBettiNumber(complex, 2);
         
         std::cout << "Betti Numbers:" << std::endl;
         std::cout << "β_0: " << betti0 << std::endl;
         std::cout << "β_1: " << betti1 << std::endl;
         std::cout << "β_2: " << betti2 << std::endl;
         return 0;
     }
     ```

10. **Find the Euler Characteristic of a Given Mesh**:
    - **Problem**: Compute the Euler characteristic of a mesh.
    - **Solution**:
      ```cpp
      #include <iostream>
      #include <vector>
      
      struct Simplex {
          std::vector<int> vertices;
      };
      
      int eulerCharacteristic(const std::vector<Simplex>& simplices) {
          int V = 0; // Number of vertices
          int E = 0; // Number of edges
          int F = 0; // Number of faces
          
          for (const auto& simplex : simplices) {
              if (simplex.vertices.size() == 1) ++V;
              else if (simplex.vertices.size() == 2) ++E;
              else if (simplex.vertices.size() == 3) ++F;
          }
          
          return V - E + F;
      }
      
      int main() {
          std::vector<Simplex> simplices = {
              {{0}}, // Vertex
              {{0, 1}}, // Edge
              {{0, 1, 2}} // Face
          };
          
          int euler = eulerCharacteristic(simplices);
          
          std::cout << "Euler Characteristic: " << euler << std::endl;
          return 0;
      }
      ```
