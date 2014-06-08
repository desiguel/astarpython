astarpython
===========

My implementation of the A* pathfinding algorithm, with text visulisations of the pathfinding in plain ASCII.

<pre>
 *000000000
 0**0000000
 777*777070
 0000*00000
 00000*0000
 000000*000
 0000000*00
 00000000*0
 00000000*0
 000000000*
</pre>

Setup
=======

You will need a board to find a path across. Some sample boards are in /boards. Passable squares are denoted by a '0' character, and impassable squares by a '7'. For the sake of simplicity, currently the start square is always the top left square (0,0) and the goal square is always the bottom right square.

Running
=======

    python search.py <board txt path> <board width> <board height>

ie:

    python search.py boards/board50obs.txt 50 50

Pseudocode
==========

This was taken from http://en.wikipedia.org/wiki/A*_search_algorithm:


`function A*(start,goal)
    closedset := the empty set    // The set of nodes already evaluated.
    openset := {start}    // The set of tentative nodes to be evaluated, initially containing the start node
    came_from := the empty map    // The map of navigated nodes.
 
    g_score[start] := 0    // Cost from start along best known path.
    // Estimated total cost from start to goal through y.
    f_score[start] := g_score[start] + heuristic_cost_estimate(start, goal)
 
    while openset is not empty
        current := the node in openset having the lowest f_score[] value
        if current = goal
            return reconstruct_path(came_from, goal)
 
        remove current from openset
        add current to closedset
        for each neighbor in neighbor_nodes(current)
            if neighbor in closedset
                continue
            tentative_g_score := g_score[current] + dist_between(current,neighbor)
 
            if neighbor not in openset or tentative_g_score < g_score[neighbor] 
                came_from[neighbor] := current
                g_score[neighbor] := tentative_g_score
                f_score[neighbor] := g_score[neighbor] + heuristic_cost_estimate(neighbor, goal)
                if neighbor not in openset
                    add neighbor to openset
 
    return failure`
    
<pre>
function reconstruct_path(came_from, current_node)
    if current_node in came_from
        p := reconstruct_path(came_from, came_from[current_node])
        return (p + current_node)
    else
        return current_node
</pre>


