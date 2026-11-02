#include <iostream>
#include <string>
#include <vector>
#include <clocale>
using namespace std;

string capitalizeName(const string& s)
{
    string result = s;
    bool newWord = true;
    for (size_t i = 0; i < result.size(); i++)
    {
        if (result[i] == ' ')
     {
            newWord = true;
        }
        else if (newWord)
        {
            if (result[i] >= 'a' && result[i] <= 'z')
                result[i] = result[i] - 32;   
            newWord = false;
        }
        }
    return result;
}
int main()
{
    setlocale(LC_ALL, "Russian");
    string line;
    cout << "Введите количество инициалов: ";
    getline(cin, line);
    int kol = stoi(line);
    vector<string> zhurnal(kol);
    cout << "Введите фамилии и имена:\n";
    for (int i = 0; i < kol; i++)
    {
        getline(cin, zhurnal[i]);
        string fixed = capitalizeName(zhurnal[i]);
        if (fixed != zhurnal[i])
        {
            cout << "  -> исправлено на: " << fixed << "\n";
            zhurnal[i] = fixed;
        }
    }
    for (int i = 0; i < kol - 1; i++)
    {
        bool swapped = false;
        for (int j = 0; j < kol - i - 1; j++)
        {
            if (zhurnal[j] > zhurnal[j + 1])
            {
                swap(zhurnal[j], zhurnal[j + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;
    }
    cout << "Вы ввели (в алфавитном порядке):\n";
    for (int i = 0; i < kol; i++)
        cout << zhurnal[i] << "\n";
}
