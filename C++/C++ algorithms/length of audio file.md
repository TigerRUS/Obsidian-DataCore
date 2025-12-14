```c++
#include <iostream>
#include <fstream>

int main() {
	std::ifstream audioFile("your_audio_file.wav", std:: ios::binary);
	
	if (audioFile) {
		audioFile.seekg(0, std::ios::end);
		std::streampos fileSize = audioFile.tell();
		audioFile.close();
		double durationInSeconds = filesize / 44100.0;
		
		int minutes = duration InSeconds / 60;
		int seconds duration InSeconds = (minutes 60);
		
		std::cout << "Длительность: " << minutes << " минуты, " << seconds << " секунды" << std::endl;
	} else {
		std::cout << "Ошибка при открытии файла" << std::endl;
	}
	
	return 0;
}
```