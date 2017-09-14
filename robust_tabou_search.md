# Robust Tabou Search

## Main loop

Parameters : 
- max_iteration_number = number of iterations
- n = size of the solution

```c
/*
    Init
*/
solution_current = get_random_solution() // init the first solution with a random permutation
solution_best = solution_current // best solution founded during the process
delta = init_delta() // Matrice of all costs
tabulist = init_tabulist() // Matrice of tabus
i_retained = infinite; // keep i when it is a better neighbor
j_retained = infinite; // keep j when it is a better neighbor
min_delta = infinite; // represent the minimal cost founded


for (k = 0 ; k < max_iteration_number ; k = k + 1){
    
    /*
        search the best neighbor and save it in i_retained and j_retained
    */
    for (i = 0; i < n-1; i = i+1){
        for (j = i+1; j < n; j = j+1){
            autorized = (tabu_list[i][p[j]] < current_iteration) || (tabu_list[j][p[i]] < current_iteration);
            
            if (autorized && delta[i][j] < min_delta){
                i_retained = i; 
                j_retained = j;
                min_delta = delta[i][j];
            }
        }
    }
    
    /*
        If we have a move, update solution, tabulist and compute 
        the updated item of the cost matrice delta
    */
    if (i_retained != infinite && j_retained != infinite){
        swap(solution_current, i_retained, j_retained)
        updateTabuList(tabulist, solution_current, i_retained, j_retained)
        
        if (i != i_retained && i != j_retained && j != i_retained && j != j_retained) {
            delta[i][j] = compute_delta_fast();
        }else{
            delta[i][j] = compute_delta();
        }
        
        if (solution_k.fitness < solution_best.fitness){
            solution_best = solution_k
        }
    } else{
        print ("All moves are tabu at iteration " + k)
    }
    
    
}

return solution_best

```
