#pragma once
#include<iostream>
#include<string>
#include"clsDate.h"
#include"clsString.h"

using namespace std;

class clsInputValidate
{
public:


	template <typename T> static bool IsNumberBetween(T Num, T From, T To)
	{
		return ((Num >= From) && (Num <= To));
	}

	static bool IsDateBetween(clsDate Date, clsDate From, clsDate To)
	{
		// Date >= From && Date <= To
		if ((clsDate::IsDate1AfterDate2(Date, From) || clsDate::IsDate1EqualDate2(Date, From))
			&&
			(clsDate::IsDate1BeforeDate2(Date, To) || clsDate::IsDate1EqualDate2(Date, To))
			)
		{
			return true;
		}

		//Date>=To && Date<=From
		if ((clsDate::IsDate1AfterDate2(Date, To) || clsDate::IsDate1EqualDate2(Date, To))
			&&
			(clsDate::IsDate1BeforeDate2(Date, From) || clsDate::IsDate1EqualDate2(Date, From))
			)
		{
			return true;
		}

		return false;

	}

	template <typename T> static T ReadNumber(string ErrorMessage = "Invalid Number, Enter again:\n")
	{
		T Number;
		while (!(cin >> Number)) {
			cin.clear();
			cin.ignore(numeric_limits<streamsize>::max(), '\n');
			cout << ErrorMessage;
		}
		return Number;
	}

	template <typename T> static T ReadNumberBetween(T From, T To, string ErrorMessage = "Number is Not within range, enter again:\n")
	{
		T Number = ReadNumber<T>();

		while (!IsNumberBetween(Number, From, To))
		{
			cout << ErrorMessage;
			Number = ReadNumber<T>();
		}
		return Number;
	}

	static	bool IsValidDate(clsDate Date)
	{
		return clsDate::IsValidDate(Date);
	}

	static string ReadString()
	{
		string S1;
		//Usage of std::ws will extract all the white spaces charecter
		getline(cin >> ws, S1);
		return S1;
	}

};