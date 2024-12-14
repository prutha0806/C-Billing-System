# C-Billing-System
#include <bits/stdc++.h>
using namespace std;


vector<int> billPrices;
vector<string> billProductNames;
vector<int> quantities;


int findPrice(int productCode, int codes[], int prices[]) {
    for (int i = 0; i < 10; i++) {
        if (productCode == codes[i]) {
            billPrices.push_back(prices[i]); 
            return prices[i];
        }
    }
    return -1; 
}


string productName(int productCode, int codes[], string groceries[]) {
    for (int i = 0; i < 10; i++) {
        if (productCode == codes[i]) {
            billProductNames.push_back(groceries[i]); 
            return groceries[i];
        }
    }
    return "Unknown Product";
}


void generateBill() {
    cout << "\n**** BILL SUMMARY ****" << endl;
    cout << "Product Name         ||  Product Price  ||  Quantity  ||  Total" << endl;
    cout << "-------------------------------------------------------------" << endl;

    int grandTotal = 0;

    for (size_t i = 0; i < billProductNames.size(); i++) {
        cout << setw(20) << left << billProductNames[i] << "||  "
             << setw(15) << left << billPrices[i] << "||  "
             << setw(10) << left << quantities[i] << "||  "
             << billPrices[i] * quantities[i] << endl;

        grandTotal += billPrices[i] * quantities[i];
    }

    cout << "-------------------------------------------------------------" << endl;
    cout << "Grand Total: " << grandTotal << endl;
}

int main() {
    int codes[10] = {101, 102, 103, 104, 105, 106, 107, 108, 109, 110};
    string groceries[10] = {"Banana", "Sugar-1kg", "Dairy Milk Chocolate", "Maida-1kg", "Wheat Flour-1kg",
                            "Rice-1kg", "Milk-1litre", "Soap", "Peanuts-200gm", "Salt-1kg"};
    int prices[10] = {60, 30, 10, 18, 15, 23, 56, 20, 82, 50};

    cout << "****WELCOME TO PRUTHA'S SUPERMARKET****" << endl;

    while (true) {
        int productCode, quant;
        cout << "\nEnter Product Code or enter 1 to exit: ";
        cin >> productCode;

        if (productCode == 1) {
            cout << "Generating bill..." << endl;
            generateBill();
            cout << "Thank you for shopping! Have a nice day!" << endl;
            break;
        }

        if (productCode < 100 || productCode > 110) {
            cout << "Invalid Product Code. Please try again." << endl;
            continue;
        }

        cout << "Enter Quantity: ";
        cin >> quant;

        quantities.push_back(quant); 
        findPrice(productCode, codes, prices); 
        productName(productCode, codes, groceries); 
    }

    return 0;
}
