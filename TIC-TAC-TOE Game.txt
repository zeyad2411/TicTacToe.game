#include<iostream>
using namespace std;

char matrix[3][3] = { {'1', '2', '3'}, {'4', '5', '6'}, {'7', '8', '9'} };
char player = 'x';

void print() {
    cout << "---------\n";
    for (int r = 0; r < 3; r++) {
        cout << "| ";
        for (int c = 0; c < 3; c++) {
            cout << matrix[r][c] << " ";
        }
        cout << "|";
        cout << endl;
    }
    cout << "---------\n";
}

void replace() {
    int position;
    cout << "Enter your position (" << player << "): ";
    cin >> position;
    if (position < 1 || position > 9) {
        cout << "Invalid position. Please try again." << endl;
        replace();
        return;
    }
    
    int row = (position - 1) / 3;
    int col = (position - 1) % 3;
    
    if (matrix[row][col] == 'x' || matrix[row][col] == 'o') {
        cout << "Position already taken. Please try again." << endl;
        replace();
        return;
    }
    
    matrix[row][col] = player;
    if (player == 'x') {
        player = 'o';
    } else {
        player = 'x';
    }
}

char winner() {
    int x = 0, o = 0, counter = 0;
    
    
    for (int r = 0; r < 3; r++) {
        x = 0;
        o = 0;
        for (int c = 0; c < 3; c++) {
            if (matrix[r][c] == 'x')
                x++;
            else if (matrix[r][c] == 'o')
                o++;
        }
        if (x == 3)
            return 'x';
        if (o == 3)
            return 'o';

        x = 0;
        o = 0;
        for (int c = 0; c < 3; c++) {
            if (matrix[c][r] == 'x')
                x++;
            else if (matrix[c][r] == 'o')
                o++;
        }
        if (x == 3)
            return 'x';
        if (o == 3)
            return 'o';
    }

    
    if (matrix[0][0] == 'x' && matrix[1][1] == 'x' && matrix[2][2] == 'x')
        return 'x';
    if (matrix[0][0] == 'o' && matrix[1][1] == 'o' && matrix[2][2] == 'o')
        return 'o';

    if (matrix[0][2] == 'x' && matrix[1][1] == 'x' && matrix[2][0] == 'x')
        return 'x';
    if (matrix[0][2] == 'o' && matrix[1][1] == 'o' && matrix[2][0] == 'o')
        return 'o';

    
    for (int r = 0; r < 3; r++) {
        for (int c = 0; c < 3; c++) {
            if (matrix[r][c] != 'x' && matrix[r][c] != 'o')
                counter++;
        }
    }
    if (counter == 0)
        return '=';

    return '*';
}

int main() {
    while (winner() == '*') {
        print();
        replace();
    }

    print();
    if (winner() == 'x') {
        cout << "The winner is player x. Congrats!" << endl;
    } else if (winner() == 'o') {
        cout << "The winner is player o. Congrats!" << endl;
    } else if (winner() == '=') {
        cout << "No one wins. It's a draw." << endl;
    }
    
    return 0;
}