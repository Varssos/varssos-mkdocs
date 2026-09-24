!!! warning
    You should remember that if you even print a map with a key that does not exist, it will add an empty pair into the map!!!

```cpp
std::map<int, std::string, std::less<int> > map = {
    {1, "Monday"},
    {2, "Tuesday"},
    {3, "Wednesday"}
};

map.insert( std::map<int, std::string>::value_type( 4, "Thursday" ));

map.insert( std::pair( 6, "Saturday" ));

std::cout << map[7];

for( auto &[number, day] : map )
{
    std::cout << number << ": " << day << '\n';
}
```
