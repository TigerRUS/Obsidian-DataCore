```c++
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>

using namespace std;

int main() {
	const string CHARS = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+[]{}<>?";
	const int PASSWORD_LENGTH = 16;
	
	srand(time(0));
	for (int i = 0; i < 5; i++)
	{
		string password = "";
		for (int j = 0; j < PASSWORD_LENGTH; j++) {
			password += CHARS [ rand() % CHARS.length()];
		}
		cout<<"Generated password " << i+1 << ": " << password << endl;
	}
	
	return 0;
}
```