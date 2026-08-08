#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdlib.h>

void display_process_info(const char *stage)
{
    printf("\n--- %s ---\n", stage);
    printf("PID  : %d\n", getpid());
    printf("PPID : %d\n", getppid());

    fflush(stdout);
}

int main()
{
    pid_t pid;

    printf("Original Process:\n");
    printf("PID  : %d\n", getpid());
    printf("PPID : %d\n", getppid());

    pid = fork();

    if (pid < 0)
    {
        perror("fork failed");
        return 1;
    }

    else if (pid == 0)
    {
        /* Child process */

        display_process_info("Child - Running");

        printf("Child is now entering waiting/sleeping state...\n");
        sleep(10);

        display_process_info("Child - Running after sleep");

        printf("Child is terminating...\n");

        exit(0);
    }

    else
    {
        /* Parent process */

        display_process_info("Parent - Running");

        printf("Child PID created by parent: %d\n", pid);

        printf("Parent is waiting for child...\n");

        wait(NULL);

        display_process_info("Parent - Running after child termination");

        printf("Parent is terminating...\n");
    }

    return 0;
}
