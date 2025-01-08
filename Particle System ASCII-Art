#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
#include <thread>
#include <chrono>

struct Particle {
    int x, y, vx, vy;
    char symbol;
};

const int WIDTH = 80;
const int HEIGHT = 20;

void clearScreen() {
    std::cout << "\033[2J\033[H";
}

void drawScreen(const std::vector<Particle>& particles) {
    std::vector<std::string> screen(HEIGHT, std::string(WIDTH, ' '));
    for (const auto& p : particles) {
        if (p.x >= 0 && p.x < WIDTH && p.y >= 0 && p.y < HEIGHT) {
            screen[p.y][p.x] = p.symbol;
        }
    }
    clearScreen();
    for (const auto& line : screen) {
        std::cout << line << "\n";
    }
}

int main() {
    srand(static_cast<unsigned>(time(0)));
    std::vector<Particle> particles;
    for (int i = 0; i < 10; ++i) {
        particles.push_back({rand() % WIDTH, rand() % HEIGHT, rand() % 3 - 1, rand() % 3 - 1, '*'});
    }

    while (true) {
        drawScreen(particles);
        for (auto& p : particles) {
            p.x += p.vx;
            p.y += p.vy;
            if (p.x <= 0 || p.x >= WIDTH - 1) p.vx = -p.vx;
            if (p.y <= 0 || p.y >= HEIGHT - 1) p.vy = -p.vy;
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }

    return 0;
}
