# fork_dasar.c

#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
int main(void) {
 int x = 100;
 printf("Mulai: PID=%d\n", getpid());
 pid_t pid = fork();
 if (pid < 0) { perror("fork"); return 1; }
 if (pid == 0) { /* proses anak */
 x += 1;
 printf("[Anak] PID=%d PPID=%d x=%d &x=%p\n",
 getpid(), getppid(), x, (void *)&x);
 } else { /* proses induk */
 wait(NULL);
 printf("[Induk] PID=%d anak=%d x=%d &x=%p\n",
 getpid(), pid, x, (void *)&x);
 }
 return 0;
}
