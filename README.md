# LabarotoryTask1
Лабораторная работа по программированию №1. Работа с разными типами данных и их представлением в памяти.
// Лабороторная по программированию №1.cpp
#include <iostream>


using namespace std;

union doubleBytes {
    double d;
    unsigned int c[2];
};
void printBinaryRepresentation(double num) { //Функция для вывода двоичного представления числа
    doubleBytes data;
    data.d = num;
    int binaryRepresentation[64];
    for (int i = 0; i < 2; ++i) { //Для каждого int в union
        for (int j = 0; j < 32; ++j) { //Для каждого бита в int
            binaryRepresentation[(1 - i) * 32 + (31 - j)] = (data.c[i] >> j) & 1;

        }
    }
    for (int i = 0; i < 64; ++i) {
        cout << binaryRepresentation[i];
        if (i == 0) {
            cout << " ";
        }
        else if (i == 12) {
            cout << " ";
        }
        else if (i == 63) {
            cout << " ";
        }

    }
    cout << endl;
};



int main()
{
    setlocale(0, "");
    int i;
    do {
        cout << "Выберите задание:" << endl;
        cout << "1) Вывести, сколько памяти (в байтах) на вашем компьютере отводится под различные типы данных со спецификаторами и без: int, short int, long int, float, double, long double, char и bool." << endl;
        cout << "2) Вывести на экран двоичное представление в памяти (все разряды) типа int. " << endl;
        cout << "3) Вывести на экран двоичное представление в памяти (все разряды) типа float." << endl;
        cout << "4) Вывести на экран двоичное представление в памяти (все разряды) типа double." << endl;
        cout << "5)ИДЗ №3: Добавить возможность неоднократно инвертировать выбранный бит для целых чисел." << endl;
        cin >> i;
        unsigned int mask1;
        unsigned int mask2;



        switch (i) {
        case 1:
            cout << "int: " << sizeof(int) << " байта" << endl << "short int: " << sizeof(short int) << " байта" << endl << "long int: " << sizeof(long int) << " байта" << endl << "float: " << sizeof(float) << " байта" << endl << "double: " << sizeof(double) << " байт" << endl << "long double: " << sizeof(long double) << " байт" << endl << "char: " << sizeof(char) << " байт" << endl << "bool: " << sizeof(bool) << " байт" << endl;
            break;
        case 2:
            int a;
            while (true) {
                cout << "Введите любое целое число: ";
                cin >> a;
                //Проверка, было ли введено целое число
                if (cin.fail()) {
                    cout << "Попробуйте снова.\n";
                    //Сбрасываем состояние cin и очищаем буфер ввода
                    cin.clear(); //сброс флага ошибок
                    cin.ignore(numeric_limits<streamsize>::max(), '\n'); //очищаем буфер
                }
                else {
                    mask1 = 1 << (sizeof(int) * 8 - 1);
                    for (int i = 1; i <= sizeof(int) * 8; i++, mask1 >>= 1) {
                        if (a & mask1) {
                            cout << "1";
                        }
                        else {
                            cout << "0";
                        }
                        if (i % 8 == 0 || i == 1) {
                            cout << " ";
                        }
                    }
                    break;

                }

            }
            break;
        case 3:
            union {
                float l;
                int b;
            };
            while (true) {
                cout << "Введите любое число с плавающей точкой: ";
                cin >> l;
                if (cin.fail()) {
                    cout << "Попробуйте снова.\n";
                    cin.clear();
                    cin.ignore(numeric_limits<streamsize>::max(), '\n');
                }
                else {
                    mask2 = 1 << (sizeof(float) * 8 - 1);
                    for (int i = 1; i <= sizeof(float) * 8; i++, mask2 >>= 1) {
                        if (b & mask2) {
                            cout << "1";
                        }
                        else {
                            cout << "0";
                        }
                        if (sizeof(float) * 8 - i == sizeof(float) * 8 - 1) {
                            cout << " ";
                        }
                        if (sizeof(float) * 8 - i == 23) {
                            cout << " ";
                        }
                    }
                    cout << "\n";
                }
                break;
            }
            break;
        case 4:
            double inputNumber;
            while (true) {
                cout << "Введите любое число с двойной точностью: ";
                cin >> inputNumber;
                if (cin.fail()) {
                    cout << "Попробуйте снова.\n";
                    cin.clear();
                    cin.ignore(numeric_limits<streamsize>::max(), '\n');
                }
                else {
                    printBinaryRepresentation(inputNumber);
                }
                break;
            }

            break;

        case 5:
            int num;
            unsigned int mask;
            cout << "Введите целое число для инвертирования: " << endl;
            int number1, mask1;
            cin >> number1;
            
                mask = 1 << (sizeof(int) * 8 - 1);
                for (int i = 0; i < sizeof(int) * 8; i++, mask >>= 1) {
                    if (number1 & mask) {
                        cout << '1';
                    }
                    else {
                        cout << '0';
                    }
                    if (i % 8 == 0) {
                        cout << " ";
                    }
                }
                cout << endl;
                cout << "Введите номер бита, который хотите инвертировать: " << endl;
                cin >> num;
                cout << endl;
                mask1 = 1 << (num - 1);
                number1 = number1 ^ mask1;
                mask = 1 << (sizeof(int) * 8 - 1);
                for (int i = 0; i < sizeof(int) * 8; i++, mask >>= 1) {

                    if (number1 & mask) {
                        cout << '1';
                    }
                    else {
                        cout << '0';
                    }
                    if (i % 8 == 0) {
                        cout << " ";
                    }
                }
                cout << endl << number1 << endl;
                break;
        default:
            cout << "Неккоректный ввод, попробуйте снова." << endl;
            break;
            }
        } while (cin >> i);    
}
