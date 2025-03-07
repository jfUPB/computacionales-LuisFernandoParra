```traduccion a C#
using System;

class HackComputer {
    const int SCREEN_SIZE = 8192; // 512 * 256 / 16
    static ushort[] SCREEN = new ushort[SCREEN_SIZE];
    static ushort KBD;

    static void HackProgram() {
        while (true) {
            if (KBD != 0) {
                for (int i = 0; i < SCREEN_SIZE; i++) {
                    SCREEN[i] = 0xFFFF; // Enciende todos los píxeles
                }
            } else {
                for (int i = 0; i < SCREEN_SIZE; i++) {
                    SCREEN[i] = 0x0000; // Apaga todos los píxeles
                }
            }
        }
    }

    static void Main() {
        HackProgram();
    }
}
```
