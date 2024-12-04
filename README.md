import random

def simulate_berkeley_algorithm(node_clocks):
    """
    Simulates the Berkeley Algorithm for clock synchronization.
    :param node_clocks: A dictionary where keys are node names and values are their clock times.
    :return: The synchronized clock times.
    """
    print("Initial Clocks:", node_clocks)

    # Step 1: Master polls the time from all nodes
    master_node = random.choice(list(node_clocks.keys()))  # Randomly select a master node
    print(f"\nMaster Node: {master_node}")

    # Calculate the average time considering round-trip delays (here we ignore network delays for simplicity)
    total_time = sum(node_clocks.values())
    average_time = total_time / len(node_clocks)

    # Step 2: Master sends the adjustments to all nodes
    adjustments = {node: average_time - time for node, time in node_clocks.items()}

    print("\nAdjustments:")
    for node, adjustment in adjustments.items():
        print(f"Node {node}: Adjust by {adjustment:.2f}")

    # Step 3: All nodes adjust their clocks
    synchronized_clocks = {node: time + adjustments[node] for node, time in node_clocks.items()}

    print("\nSynchronized Clocks:", synchronized_clocks)
    return synchronized_clocks


# Example usage
if __name__ == "__main__":
    # Initial clock times (in seconds or minutes, for example)
    node_clocks = {
        "Node1": 100,
        "Node2": 110,
        "Node3": 90,
        "Node4": 105
    }

    simulate_berkeley_algorithm(node_clocks)
