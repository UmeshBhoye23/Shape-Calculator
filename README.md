# Shape-Calculator
#include <iostream>
#include <cmath>


using namespace std;

const double PI = 3.14;

class Shape
{
public:
    virtual void showShape() const = 0;
    virtual void getSizes() = 0;
    virtual double calculateArea() const = 0;
    virtual double calculatePerimeter() const = 0;
    virtual double calculateDiagonal() const { return 0; }
    virtual void showImg() const = 0;
    virtual void showImgEdges() const = 0;
    virtual ~Shape() {}
};

class Rectangle : public Shape
{
private:
    double length, width;

public:
    void showShape() const override
    {
        cout << "------------------------\n";
        cout << "        Rectangle       \n";
        cout << "------------------------\n";
    }

    void getSizes() override
    {
        cout << "- Enter length: ";
        cin >> length;
        cout << "- Enter width : ";
        cin >> width;
    }

    double calculateArea() const override
    {
        return length * width;
    }

    double calculatePerimeter() const override
    {
        return 2 * (length + width);
    }

    double calculateDiagonal() const override
    {
        return sqrt(pow(length, 2) + pow(width, 2));
    }

    void showImg() const override
    {
        const int maxDisplaySize = 10;

        double scale = min(1.0, maxDisplaySize / max(length, width));

        cout << "\nImage Representation:\n\n";
        for (int i = 0; i < length * scale; i++)
        {
            cout << "    ";
            for (int j = 0; j < width * scale; j++)
            {
                cout << "* ";
            }
            cout << endl;
        }
        cout << endl;
    }

    void showImgEdges() const override
    {
        cout << "\nPerimeter Representation:\n\n";
        for (int i = 0; i < width; i++)
        {
            cout << "* ";
        }
        cout << endl;

        for (int i = 1; i < length - 1; i++)
        {
            cout << "* ";
            for (int j = 1; j < width - 1; j++)
            {
                cout << "  ";
            }
            cout << "*\n";
        }

        for (int i = 0; i < width; i++)
        {
            cout << "* ";
        }
        cout << endl;
        cout << endl;
    }
};

class Circle : public Shape
{
private:
    double radius;

public:
    void showShape() const override
    {
        cout << "------------------------\n";
        cout << "         Circle         \n";
        cout << "------------------------\n";
    }

    void getSizes() override
    {
        cout << "- Enter radius: ";
        cin >> radius;
    }

    double calculateArea() const override
    {
        return PI * pow(radius, 2);
    }

    double calculatePerimeter() const override
    {
        return 2 * PI * radius;
    }

    void showImg() const override
    {
        const int maxDisplaySize = 10;

        double scale = min(1.0, maxDisplaySize / (2 * radius + 1));

        int diameter = 2 * (radius * scale) + 1;
        cout << "\nImage Representation:\n\n";
        for (int i = -radius * scale; i <= radius * scale; i++)
        {
            cout << "    ";
            for (int j = -radius * scale; j <= radius * scale; j++)
            {
                if (sqrt(i * i + j * j) <= radius * scale + 0.5)
                {
                    cout << "* ";
                }
                else
                {
                    cout << "  ";
                }
            }
            cout << endl;
        }
        cout << endl;
    }

    void showImgEdges() const override
    {
        const int maxDisplaySize = 10;

        double scale = min(1.0, maxDisplaySize / (2 * radius + 1));

        int diameter = 2 * (radius * scale) + 1;
        cout << "\nCircumference Representation:\n\n";
        for (int i = -radius * scale; i <= radius * scale; i++)
        {
            cout << "    ";
            for (int j = -radius * scale; j <= radius * scale; j++)
            {
                if (sqrt(i * i + j * j) <= radius * scale + 0.5 && sqrt(i * i + j * j) >= radius * scale - 0.5)
                {
                    cout << "* ";
                }
                else
                {
                    cout << "  ";
                }
            }
            cout << endl;
        }
        cout << endl;
    }
};

class Triangle : public Shape
{
private:
    double base, height;

public:
    void showShape() const override
    {
        cout << "------------------------\n";
        cout << "       Triangle \n";
        cout << "------------------------\n";
    }

    void getSizes() override
    {
        cout << "- Enter base  : ";
        cin >> base;
        cout << "- Enter height: ";
        cin >> height;
    }

    double calculateArea() const override
    {
        return 0.5 * base * height;
    }

    double calculatePerimeter() const override
    {
        return 3 * base;
    }

    void showImg() const override
    {
        cout << "\nImage Representation:\n\n";
        for (int i = 0; i < height; i++)
        {
            for (int j = 0; j < height - i - 1; j++)
            {
                cout << " ";
            }
            for (int k = 0; k < 2 * i + 1; k++)
            {
                cout << "*";
            }
            cout << endl;
        }
        cout << endl;
    }

    void showImgEdges() const override
    {
        for (int i = 0; i < height - 1; i++)
        {
            for (int j = 0; j < height - i - 1; j++)
            {
                cout << " ";
            }

            for (int j = 0; j < 2 * i + 1; j++)
            {
                if (j == 0 || j == 2 * i)
                {
                    cout << "*";
                }
                else
                {
                    cout << " ";
                }
            }

            cout << endl;
        }

        for (int i = 0; i < 2 * height - 1; i++)
        {
            cout << "*";
        }

        cout << endl;
    }
};

class Square : public Shape
{
private:
    double side;

public:
    void showShape() const override
    {
        cout << "------------------------\n";
        cout << "         Square         \n";
        cout << "------------------------\n";
    }

    void getSizes() override
    {
        cout << "- Enter side length: ";
        cin >> side;
    }

    double calculateArea() const override
    {
        return pow(side, 2);
    }

    double calculatePerimeter() const override
    {
        return 4 * side;
    }

    double calculateDiagonal() const override
    {
        return side * sqrt(2);
    }

    void showImg() const override
    {
        cout << "\nImage Representation:\n\n";
        for (int i = 0; i < side; i++)
        {
            cout << "    ";
            for (int j = 0; j < side; j++)
            {
                cout << "* ";
            }
            cout << endl;
        }
        cout << endl;
    }

    void showImgEdges() const override
    {
        cout << "\nPerimeter Representation:\n\n";
        for (int i = 0; i < side; i++)
        {
            cout << "* ";
        }
        cout << endl;

        for (int i = 1; i < side - 1; i++)
        {
            cout << "* ";
            for (int j = 1; j < side - 1; j++)
            {
                cout << "  ";
            }
            cout << "*\n";
        }

        for (int i = 0; i < side; i++)
        {
            cout << "* ";
        }
        cout << endl;
        cout << endl;
    }
};

void process(Shape &shape)
{
    shape.showShape();
    shape.getSizes();

    char option;
    cout << "\nWhat do you want to find?\n";
    cout << "  a - Area\n";
    cout << "  p - Perimeter\n";
    cout << "  d - Diagonal (if applicable)\n";
    cout << "  f - All Features\n";
    cout << "Choose: ";
    cin >> option;

    switch (option)
    {
    case 'a':
        cout << "\nArea is: " << shape.calculateArea() << endl;
        shape.showImg();
        break;
    case 'p':
        cout << "\nPerimeter is: " << shape.calculatePerimeter() << endl;
        shape.showImgEdges();
        break;
    case 'd':
        cout << "\nDiagonal is: " << shape.calculateDiagonal() << endl;
        shape.showImg();
        break;
    case 'f':
        cout << "\nFeatures:\n";
        cout << "- Area: " << shape.calculateArea() << endl;
        cout << "- Perimeter: " << shape.calculatePerimeter() << endl;
        cout << "- Diagonal: " << shape.calculateDiagonal() << endl;
        cout << "- Image Representation:\n";
        shape.showImg();
        shape.showImgEdges();
        break;
    default:
        cout << "\nInvalid choice! Try again.\n";
        break;
    }
}

int main()
{
    char choice;

    while (true)
    {
        cout << "\nWelcome to the 2D Shapes Calculator!\n";
        cout << "Choose a shape:\n";
        cout << "  r - Rectangle\n";
        cout << "  c - Circle\n";
        cout << "  t - Triangle\n";
        cout << "  s - Square\n";
        cout << "  q - Quit\n";
        cout << "Your choice: ";
        cin >> choice;

        if (choice == 'q')
        {
            cout << "\nExiting...\n";
            break;
        }

        switch (choice)
        {
        case 'r':
        {
            Rectangle rectangle;
            process(rectangle);
            break;
        }
        case 'c':
        {
            Circle circle;
            process(circle);
            break;
        }
        case 't':
        {
            Triangle triangle;
            process(triangle);
            break;
        }
        case 's':
        {
            Square square;
            process(square);
            break;
        }
        default:
            cout << "\nInvalid shape! Choose again \n";
            continue;
        }
    }

    return 0;
}
