# !!! DO NOT USE !!!
**This library invokes undefined behavior, and should not be used unless fixed!**

See [issue#8](https://github.com/Leandros/MariaDB-Connector-Cxx/issues/8) for more information.


# MariaDB Connector/C++

Connector/C++ is a C++ wrapper for the functionality of the [MariaDB Connector/C library](https://github.com/MariaDB/mariadb-connector-c).

### Motivations
The advertised C++ library for MariaDB is old, unmaintained and cumbersome to use. Furthermore it depends on Boost, and also exposed a lot of the C API data structures to the user.
The goal of this library is a streamlined, and good experience for the user. It should be easy to use, without sacrificing the performance.


### Features
- Easy to use
- Doesn't expose any data structure of the C API to the user
- Fully object oriented
- LGPL, free to use for anyone.
- No dependencies on STL containers
- No dependencies on Boost
- Easy to replace allocators (only uses `malloc` and `free`)

# Dependencies
- [MariaDB Connector/C](https://github.com/MariaDB/mariadb-connector-c)

# Usage

	#include "MySQLCXX.h"
	#include <stdio.h>
	#include <string.h>
	
	int main()
	{
	    Connection Con;
		Con.Connect("localhost", "root", "root", NULL, 3306);
		if (Con.IsConnected())
		{
		    Result Res;
		    char const* query = SQL(
			    SELECT `name`,`age`
			    FROM `test`);
	        int NumRows = Con->Query(query, strlen(query), &Res);
	        if (NumRows > 0)
	        {
	            Row* Row0 = Res.GetRow(0);
		        Field* Name = Row0->GetField(0);
		        Field* Age = Row0->GetField(1);
		        printf("%s is %d years old.\n", Name->AsString(), Age->AsUnsignedByte());
		    }
	    }
	    
	    return 0;
	}

For more examples, see the [`Tests.cpp`](https://github.com/Leandros/MariaDB-Connector-Cxx/blob/master/tests/Tests.cpp).

# Contributing
Feel free to contribute. A good start is to browse the ["help wanted"](https://github.com/Leandros/MariaDB-Connector-Cxx/labels/help%20wanted) tag, there are a few open issues I would love to see some contributions.

# Author
MariaDB Connector/C++ was written by [Arvid Gerstmann](https://github.com/Leandros).

# License
MariaDB Connector/C++ is licensed under [LGPL v2.1 or higher](https://github.com/Leandros/MariaDB-Connector-Cxx/blob/master/LICENSE). See the [`LICENSE`](https://github.com/Leandros/MariaDB-Connector-Cxx/blob/master/LICENSE) file for more.

# Is it any good?
[Yes.](https://news.ycombinator.com/item?id=3067434)
