#include <iostream>

class string
{
private:
	char* str;
	int size;

	void add_str(const char* str)
	{
		size = strlen(str);
		this->str = new char[size + 1];
		for (int i = 0; i < size + 1; ++i)
			this->str[i] = str[i];
	}
public:
	string()
	{
		str = nullptr;
		size = 0;
	}

	string(const char* str)
	{
		//add_str(s);
		this->size = strlen(str);
		this->str = new char[this->size + 1];
		for (int i = 0; i <= this->size; ++i)
			this->str[i] = str[i];
		//*this->str = *str;
	}

	void operator = (char* str)
	{
		this->size = strlen(str);
		this->str = new char[this->size + 1];
		for (int i = 0; i < this->size; ++i)
			this->str[i] = str[i];
	}

	string(const string& other)
	{
		//add_str(other.str);
		this->size = other.size;
		this->str = other.str;
	}

	/*string(string&& other)
	{
		this->size = other.size;
		this->str = other.str;
		other.str = nullptr;
	}*/

	/*string& operator = (const string& other)
	{
		if (this->str != nullptr)
		{
			delete[] str;
			size = 0;
		}
		add_str(other.str);
		return *this;
	}*/

	void operator = (string& other)
	{
		this->str = other.str;
		this->size = other.size;
		other.str = nullptr;
	}

	string operator + (const string& other)
	{
		string new_str;
		new_str.size = other.size + this->size;
		new_str.str = new char[new_str.size + 1];
		for (int i = 0; i < this->size; ++i)
			new_str.str[i] = this->str[i];
		for (int i = this->size; i < new_str.size + 1; ++i)
			new_str.str[i] = other.str[i - this->size];
		return new_str;
	}

	string& operator += (const string& other)
	{
		string new_str;
		new_str.size = other.size + this->size;
		new_str.str = new char[new_str.size + 1];
		for (int i = 0; i < this->size; ++i)
			new_str.str[i] = this->str[i];
		for (int i = this->size; i < new_str.size + 1; ++i)
			new_str.str[i] = other.str[i - this->size];
		delete[] this->str;
		this->str = new_str.str;
		this->size = new_str.size;
		new_str.str = nullptr;
		return *this;
	}

	bool operator == (const string& other)
	{
		if (this->size != other.size)
			return 0;
		for (int i = 0; i < this->size; ++i)
		{
			if (this->str[i] != other.str[i])
				return 0;
		}
		return 1;
	}

	bool operator != (const string& other)
	{
		//return!(this->operator== other);
		if (this->size != other.size)
			return 1;
		for (int i = 0; i < this->size; ++i)
		{
			if (this->str[i] != other.str[i])
				return 1;
		}
		return 0;
	}

	void operator << (const string& other)
	{
		for (int i = 0; i < other.size; ++i)
			std::cout << other.str[i];
	}

	char& operator [] (const int& i)
	{
		return this->str[i];
	}

	friend std::ostream& operator<< (std::ostream& out, const string& other)
	{
		out << other.str;
		return out;
	}

	friend std::istream& operator >>(std::istream& in, string& other)
	{
		in >> other.str;
		return in;
	}

	int length()
	{
		return size;
	}

	void clear()
	{
		delete[] this->str;
	}

	bool empty()
	{
		if (this->str == nullptr)
			return 1;
		return 0;
	}

	~string()
	{
		delete[] this->str;
	}
};



int main()
{
	string s1("test");
	string s2(s1);
	s1 += s2;
	std::cout << s1 << std::endl;
	//s1 = s2;
	std::cout << s2[1]<<std::endl;
	string s3= s1 + s2;
	std::cout << s3<<std::endl;
	std::cout << (s1 == s2)<<' '<<(s1!=s2)<<std::endl;
	//const char* chr = "fgb";
	//string s3 = chr;
	string s4 = s1 + s2+s3;
	std::cout << s4 << std::endl;
	string s5(s1 + s2);
	std::cout << s5 << std :: endl;
  string s6 = "loshok";
  std::cout << s6;
}
