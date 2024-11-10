#include <stdio.h>

struct Process {
    int id;         // Process ID
    int arrival;    // Arrival time
    int burst;      // Burst time (time required for execution)
    int completion; // Completion time
    int waiting;    // Waiting time
    int turnaround; // Turnaround time
};

void findWaitingTime(struct Process processes[], int n) {
    processes[0].waiting = 0; // The first process has no waiting time

    for (int i = 1; i < n; i++) {
        processes[i].waiting = processes[i-1].completion - processes[i].arrival;
        if (processes[i].waiting < 0)
            processes[i].waiting = 0; // If waiting time is negative, set to 0
    }
}

void findTurnaroundTime(struct Process processes[], int n) {
    for (int i = 0; i < n; i++) {
        processes[i].turnaround = processes[i].burst + processes[i].waiting;
    }
}

void findCompletionTime(struct Process processes[], int n) {
    processes[0].completion = processes[0].arrival + processes[0].burst;
    for (int i = 1; i < n; i++) {
        processes[i].completion = processes[i-1].completion + processes[i].burst;
    }
}

void findAverageTimes(struct Process processes[], int n) {
    int totalWaiting = 0, totalTurnaround = 0;

    for (int i = 0; i < n; i++) {
        totalWaiting += processes[i].waiting;
        totalTurnaround += processes[i].turnaround;
    }

    printf("Average waiting time: %.2f\n", (float)totalWaiting / n);
    printf("Average turnaround time: %.2f\n", (float)totalTurnaround / n);
}

void printProcessDetails(struct Process processes[], int n) {
    printf("Process ID | Arrival Time | Burst Time | Completion Time | Waiting Time | Turnaround Time\n");
    for (int i = 0; i < n; i++) {
        printf("%10d | %12d | %10d | %15d | %12d | %15d\n", 
               processes[i].id, processes[i].arrival, processes[i].burst,
               processes[i].completion, processes[i].waiting, processes[i].turnaround);
    }
}

int main() {
    int n;

    // Take number of processes as input
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    struct Process processes[n];

    // Input process details
    for (int i = 0; i < n; i++) {
        processes[i].id = i + 1;
        printf("\nEnter arrival time and burst time for process %d: ", i + 1);
        scanf("%d %d", &processes[i].arrival, &processes[i].burst);
    }

    // Sort processes by arrival time
    struct Process temp;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (processes[i].arrival > processes[j].arrival) {
                temp = processes[i];
                processes[i] = processes[j];
                processes[j] = temp;
            }
        }
    }

    // Calculate completion, waiting, and turnaround times
    findCompletionTime(processes, n);
    findWaitingTime(processes, n);
    findTurnaroundTime(processes, n);

    // Display process details and average times
    printProcessDetails(processes, n);
    findAverageTimes(processes, n);

    return 0;
}
