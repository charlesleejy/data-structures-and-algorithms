## Gas Station

### Problem Description
There are `n` gas stations along a circular route, where the amount of gas at the `i-th` station is `gas[i]`. You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `i-th` station to its next `(i + 1)-th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique.

### Example
```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 units of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. Your tank = 5 - 5 + 4 = 4
The starting point 3 has enough gas to travel around the circuit once.
```
```
Input: gas = [2,3,4], cost = [3,4,3]
Output: -1
Explanation:
You can't start at any station and make a complete circuit.
```

### Solution Approach
To solve this problem, we can use a greedy approach. The idea is to keep track of the total gas and cost to determine if a solution is possible, and use a greedy strategy to find the starting station.

### Steps in Detail

1. **Check Feasibility**:
   - If the total amount of gas is less than the total cost, it is impossible to complete the circuit, so return -1.

2. **Greedy Approach to Find Starting Station**:
   - Use two variables: `total_tank` and `current_tank`.
   - `total_tank` keeps track of the total net gas after traversing all stations.
   - `current_tank` keeps track of the net gas of the current route.
   - Initialize `starting_station` to 0.
   - Traverse each station and update `total_tank` and `current_tank`.
   - If `current_tank` drops below 0, it means the car cannot continue from the current starting station, so update `starting_station` to the next station and reset `current_tank` to 0.

### Python Code
```python
def can_complete_circuit(gas, cost):
    if sum(gas) < sum(cost):
        return -1
    
    total_tank, current_tank = 0, 0
    starting_station = 0
    
    for i in range(len(gas)):
        total_tank += gas[i] - cost[i]
        current_tank += gas[i] - cost[i]
        
        if current_tank < 0:
            starting_station = i + 1
            current_tank = 0
    
    return starting_station if total_tank >= 0 else -1
```

### Java Code
```java
public class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalTank = 0, currentTank = 0;
        int startingStation = 0;
        
        for (int i = 0; i < gas.length; i++) {
            totalTank += gas[i] - cost[i];
            currentTank += gas[i] - cost[i];
            
            if (currentTank < 0) {
                startingStation = i + 1;
                currentTank = 0;
            }
        }
        
        return totalTank >= 0 ? startingStation : -1;
    }
}
```

### Explanation

1. **Check Feasibility**:
   - In Python, we use `sum(gas) < sum(cost)` to check if the total gas is less than the total cost. If it is, we return -1.
   - In Java, this check is implicit as we calculate the `totalTank` in the loop.

2. **Greedy Approach to Find Starting Station**:
   - Initialize `total_tank`, `current_tank`, and `starting_station` to 0.
   - Traverse each station:
     - Update `total_tank` and `current_tank` by adding the difference between the gas at the current station and the cost to reach the next station.
     - If `current_tank` drops below 0, it means the current starting station cannot reach the next station:
       - Update `starting_station` to the next station (`i + 1`).
       - Reset `current_tank` to 0.
   - After the loop, if `total_tank` is non-negative, return `starting_station`; otherwise, return -1.

This approach ensures that we traverse the array only once, making it an O(n) solution, and we use only O(1) extra space for the variables `total_tank`, `current_tank`, and `starting_station`.