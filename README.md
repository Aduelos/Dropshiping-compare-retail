#include <iostream>
#include <vector>
#include <string>
#include <limits>

struct Product {
    std::string name;
    double price;
    double shippingCost;
    int rating; // Évalué sur 5

    double totalCost() const {
        return price + shippingCost;
    }
};

void compareProducts(const std::vector<Product>& products) {
    if (products.empty()) {
        std::cout << "Aucun produit à comparer." << std::endl;
        return;
    }

    const Product* bestProduct = &products[0];

    for (const auto& product : products) {
        if (product.totalCost() < bestProduct->totalCost()) {
            bestProduct = &product;
        }
    }

    std::cout << "Le meilleur produit est: " << bestProduct->name << std::endl;
    std::cout << "Prix: " << bestProduct->price << " USD" << std::endl;
    std::cout << "Coût d'expédition: " << bestProduct->shippingCost << " USD" << std::endl;
    std::cout << "Évaluation: " << bestProduct->rating << "/5" << std::endl;
    std::cout << "Coût total: " << bestProduct->totalCost() << " USD" << std::endl;
}

int main() {
    std::vector<Product> products;
    int n;

    std::cout << "Combien de produits voulez-vous comparer ? ";
    std::cin >> n;

    for (int i = 0; i < n; ++i) {
        Product product;
        std::cout << "Entrez le nom du produit " << (i + 1) << ": ";
        std::cin >> product.name;

        std::cout << "Entrez le prix du produit " << (i + 1) << " (en USD): ";
        std::cin >> product.price;

        std::cout << "Entrez le coût d'expédition du produit " << (i + 1) << " (en USD): ";
        std::cin >> product.shippingCost;

        std::cout << "Entrez l'évaluation du produit " << (i + 1) << " (sur 5): ";
        std::cin >> product.rating;

        products.push_back(product);
    }

    compareProducts(products);

    return 0;
}

