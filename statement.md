# description: 
 The program is ill-formed.  The return type of the virtual function that is called dynamically is converted to the return type of the overridden function.  In this case the result of the duplicate() function is a pointer to a Box object but converted to a Shape pointer.  Therefore the assignment from the return value to b1 is ill-formed.
```C++ runnable
#include <iostream>

struct Shape
{
  virtual Shape* duplicate()
  {
    return new Shape;
  }
  virtual void print()
  {
    std::cout << "SHAPE" << std::endl;
  }
  virtual ~Shape() {}
};

struct Box : public Shape
{
  virtual Box* duplicate()
  {
    return new Box;
  }
  virtual void print()
  {
    std::cout << "BOX" << std::endl;
  }
};

int main(int argc, char** argv) 
{ 
  Shape* s1 = new Box;

  Box* b1 = s1->duplicate();

  b1->print();

  delete s1;
  delete b1;
  return 0; 
}
