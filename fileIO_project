#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

// 비밀번호를 입력받아서
// 맞는 경우 - 비밀 노트를 보여주고 내용을 저장.
// 틀린 경우 - 경고 메세지를 표시하고 종료.

char password[20];
char confirm_password[20];
char using_password[20];
#define MAX 10000

int clear_password(int i, char password[20], char confirm_password[20]);

int main(void) {

	char line[MAX]; // 파일에서 불러온 내용을 저장할 변수
	char contents[MAX]; // 일기장에 입력할 내용
	char initpassword = 0;
	char c; // 비밀번호 입력할 때 확인용
	int i = 0;

	// fgets, fputs 활용

	if (initpassword == 0) {
		printf("비밀노트에 오신 것을 환영합니다.\n");
		
		// 초기 비밀번호 설정
password:
		printf("\n사용하실 비밀번호를 입력하세요.\n");
		printf("비밀번호는 영문자 최대 20자, 한글 최대 10자까지 가능합니다.\n");
		while (1) {
			c = getch(); // 한 자씩 입력할 때마다 수행(c에 임의의 값을 입력받음)
			if (c == 13) { // 13 == Enter - > 비밀번호 입력 종료
				password[i] = '\0';
				break;
			}
			else if (c == 8) {
				// 비밀번호 잘못 입력시 백스페이스
				printf("\b");
				printf(" ");
				printf("\b");

				if (i > 0) {
					i--;
				}
			}
			else { // 입력한 비밀번호를 *로 표시
				printf("*");
				password[i] = c;
				i++;
			}
		}

		// 비밀번호 확인
		printf("\n비밀번호를 한 번 더 입력해 주세요.\n");
confirm_password:
		i = 0;
		while (1) {
			c = getch(); // 한 자씩 입력할 때마다 수행(c에 임의의 값을 입력받음)
			if (c == 13) { // 13 == Enter - > 비밀번호 입력 종료
				password[i] = '\0';
				break;
			}
			else if (c == 8) {
				// 비밀번호 잘못 입력시 백스페이스
				printf("\b");
				printf(" ");
				printf("\b");

				if (i > 0) {
					i--;
				}
			}
			else if (c == 27) { // 비밀번호 다시 설정 - esc
				clear_password(i, password, confirm_password); // 기존에 입력한 패스워드 초기화
				goto password;
			}
			else { // 입력한 비밀번호를 *로 표시
				printf("*");
				confirm_password[i] = c;
				i++;
			}
		}

		for (int j = 0; j < i + 1; j++) {
			if (password[j] != confirm_password[j]) {
				printf("\n비밀번호가 서로 일치하지 않습니다.\n");
				printf("비밀번호를 처음부터 다시 입력하려면 esc 키를 눌러주세요.\n\n");
				goto confirm_password;
			}
		}
		printf("\n비밀번호가 설정되었습니다.\n");
		initpassword = 1;
	}

	// 초기 비밀번호 설정 이후에 실행시켰을 때
		if (initpassword == 1) {
		printf("\n\n비밀노트에 오신 것을 환영합니다.\n");
		printf("비밀번호를 입력하세요.\n");

password2:
		i = 0;
		while (1) {
			c = getch(); // 한 자씩 입력할 때마다 수행(c에 임의의 값을 입력받음)
			if (c == 13) { // 13 == Enter - > 비밀번호 입력 종료
				password[i] = '\0';
				break;
			}
			else if (c == 8) {
				// 비밀번호 잘못 입력시 백스페이스
				printf("\b");
				printf(" ");
				printf("\b");

				if (i > 0) {
					i--;
				}
			}
			else { // 입력한 비밀번호를 *로 표시
				printf("*");
				using_password[i] = c;
				i++;
			}
		}
		for (int j = 0; j < i + 1; j++) {
			if (using_password[j] != confirm_password[j]) {
				printf("\n비밀번호가 일치하지 않습니다.\n");
				goto password2;
			}
		}
	}
	printf("\n로그인 성공\n\n");

	char* fileName = "d:\secretnotetxt";
	FILE* file = fopen(fileName, "a+b"); // a+b: 파일이 없으면 생성, 파일이 있으면 뒤에 내용을 추가함.
	
	if (file == NULL) {
		printf("파일 열기 실패\n");
		return 1;
	}
	while (fgets(line, MAX, file) != NULL) { // file에서 line으로 불러올 값이 있으면
		printf("%s", line);
	}
	printf("\n\n내용을 계속 작성하세요.(종료: exit 입력)\n\n");
	
	while (1) {
		scanf("%[^\n]", contents); // 새 줄(\n)이 나오기 전까지 읽어들임.(한 문장씩 저장)
		// %[scanlist]: scanlist의 위치에 해당되는 곳의 문자만 읽어들임. %[^123]에서 2 5 7입력: 2만 읽음.
		getchar(); // 버퍼에 남아있는 \n을 Flush 처리.
		
		if (strcmp(contents, "exit") == 0) {
			printf("노트 작성을 종료합니다.\n");
			break;
		}
		fputs(contents, file);
		fputs("\n", file); // Enter를 위에서 무시 처리하였으므로 임의로 추가.
	}
	fclose(file);
	return 0;
}
int clear_password(int i, char password[20], char confirm_password[20]) { // 비밀번호 초기화
	password[20] = "";
	confirm_password[20] = "";
}
