# std::string

## Strip terminator from ending

```cpp
const std::string MESSAGE_ENDING{ "\x17\r\n>" };

std::string StripTerminator( const std::string &aMsg )
{
    std::string lResult;
    if( aMsg.length() >= MESSAGE_ENDING.length() &&
        std::string_view( aMsg.cend().base() - MESSAGE_ENDING.length(), MESSAGE_ENDING.length() ) == MESSAGE_ENDING )
    {
        lResult = aMsg.substr( 0, aMsg.size() - MESSAGE_ENDING.length() );
    }
    return lResult;
}

int main()
{
    std::string lReceivedMessage { "N, 1097429\x17\r\n>" };

    lReceivedMessage = StripTerminator( lReceivedMessage );

    return 0;
}
```

## Verify if a string contains a substring/char

```cpp
bool ContainComma( const std::string &aReceivedMessage )
{
    if( aReceivedMessage.find(',') != std::string::npos )
    {
        return true;
    }

    return false;
}
```

## Check if a string contains only numbers

```cpp
bool isNumber( const std::string &str )
{
    return str.find_first_not_of( "0123456789" ) == std::string::npos;
}

bool isNumber(const std::string &s) 
{
    return !s.empty() && std::all_of(s.begin(), s.end(), ::isdigit);
}

bool isNumber(const std::string& s)
{
    return !s.empty() && std::find_if(s.begin(),
        s.end(), [](unsigned char c) { return !std::isdigit(c); }) == s.end();
}
```
