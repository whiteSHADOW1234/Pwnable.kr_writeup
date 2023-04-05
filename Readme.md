# Pwnable.kr
- a quick writeup for [this website](http://pwnable.kr/play.php)

## 1. fd
### Solution by steps
1. Get to [this website (an online ssh terminal)](https://www.redcoolmedia.net/sshgate/)
2. And enter the URL, Port, UserName, and the password
![](https://i.imgur.com/06bxS9F.png)

3. Then, after running `ls` you'll see there are three files in the derectory: `fd`, `fd.c`, `flag`
4. Run `cat flag` but get `Permission denied`
5. So `cat fd.c` and find this:
```c 
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
char buf[32];
int main(int argc, char* argv[], char* envp[]){
        if(argc<2){
                printf("pass argv[1] a number\n");
                return 0;
        }
        int fd = atoi( argv[1] ) - 0x1234;
        int len = 0;
        len = read(fd, buf, 32);
        if(!strcmp("LETMEWIN\n", buf)){
        int len = 0;
        len = read(fd, buf, 32);
        if(!strcmp("LETMEWIN\n", buf)){
        int len = 0;
        len = read(fd, buf, 32);
        if(!strcmp("LETMEWIN\n", buf)){
                printf("good job :)\n");
                system("/bin/cat flag");
                exit(0);
        }
        printf("learn about Linux file IO\n");
        return 0;
}

```
6. Run `python` and type in `int(0x1234)` to get the number to pass in: `4660`
7. Enter `./fd 4660` and `LETMEWIN`, you'll get this:
![](https://i.imgur.com/9VnJp1d.png)
8. And that's you flag ~ :smile: 

## 2. 




