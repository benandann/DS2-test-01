//********************************************************************************/ 
// DS2ex01_18_10727217陳炯瑋_10727223陳宇呈 
//********************************************************************************/ 

#include <stdio.h>
#include <iostream>
#include <string.h>
#include <cstdio>
#include <stdlib.h>
#include <vector>
#include <fstream>
#include <algorithm>

using namespace std ;

struct inform {
	string schOid ;
	string schName ;
	string depOid ;
	string depName ;
	string day ;
	string dayName ;
	string level ;
	string levelName ;
	string studentNum ;
	string teacherNum ;
	int graduator ;
	string countryNum ;
	string country ;
	string typeNum ;
	string type ;
	int list ;
};

struct sortinform {
	int list ;
	int graduator ;
};


class Job1 {
	public:
		vector<inform> store ;
		vector<sortinform> sorted ;
		
		void Init() {
			store.clear() ;
			sorted.clear() ;
		} // Init
		
		int DataSize() {
			return store.size() ;
		} // DataSize
		
		void Readfile( string file_name ) {
				int i = 1 ;
				int size = 1000 ;
				char * line  = new char[size] ; // 讀垃圾
				char * testinform = new char[size] ;
				inform tempinform ;
				FILE * file ;
				string tempfile_name = file_name ;
			    tempfile_name = "input" + file_name + ".txt" ;
				file = fopen( tempfile_name.c_str(), "r" ) ;
				if ( file == NULL )
				    cout << "### " << tempfile_name << " does not exist! ###" << endl ;
			    else {
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
		    	
					while ( fscanf( file, "%s", testinform ) != EOF ) {
						tempinform.schOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.schName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.day = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.dayName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.level = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.levelName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.studentNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.teacherNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.graduator = atoi(testinform) ;
						fscanf( file, "%s", testinform ) ;
						tempinform.countryNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.country = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.typeNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.type = testinform ;
						
						tempinform.list = i ;
						i++ ;
					
						store.push_back( tempinform ) ;
					} // while
				
					delete [] line ;
					delete [] testinform ;
					fclose( file ) ;
				} // else
			
			} // Readfile
			
			void test () {
				int site = 0, size = sorted.size() ;
				for ( ; site < size ; site++ ) {
					cout << sorted.at(site).list << "\t" << sorted.at(site).graduator << endl ;
				} // for
			} // test
		
			// **********************************任務一*********************************************** 
			
			void compare ( int now ) {
				while ( now > 0 ) {
					int parent = ( now-1 ) / 2 ;
					if ( sorted.at(now).graduator < sorted.at(parent).graduator ) {
						swap( sorted.at(now), sorted.at(parent) ) ;
						now = parent ;
						parent = ( now-1 ) / 2 ;
					} // if
					else {
						break ; // 沒交換就跳出迴圈 
					} // else
					
				} // while
				
			} // compare
			
			void sorting () {
				// *******************先放第一筆資料**************************
				sortinform tempinform ;
				tempinform.graduator = store.at(0).graduator ;
				tempinform.list = store.at(0).list ;
				sorted.push_back( tempinform ) ; 
				
				// *******************邊放邊比較******************************
				
				int num = 1 ;
				while ( num < DataSize() ) {
					tempinform.graduator = store.at(num).graduator ;
					tempinform.list = store.at(num).list ;
					sorted.push_back( tempinform ) ;
					compare( num ) ;
					num++ ; 
				} // while
				
				num-- ; // bottom位置
				 
				// *******************找最左邊節點***************************** 
				
				int point = num ;
				int count = 0 ;
				while ( point > 0 ) {
					point = ( point-1 ) / 2 ;
					count++ ; // 算在第幾層 
				} // while
				
				while ( count > 0 ) {
					point = point * 2 + 1 ;
					count-- ;
				} // while	 
				 
				// *******************印出數據********************************** 
				
				cout << "root: [" << sorted.at(0).list << "] " << sorted.at(0).graduator << "\n" ;
				cout << "bottom: [" << sorted.at(num).list << "] " << sorted.at(num).graduator << "\n" ;
				cout << "leftmost bottom: [" << sorted.at(point).list << "] " << sorted.at(point).graduator << "\n" ;	
				
			} // sorting
			
			
}; 

class Job2 {
	public:
		vector<inform> store ;
		vector<sortinform> sorted ;
		
		void Init() {
			store.clear() ;
			sorted.clear() ;
		} // Init
		
		int DataSize() {
			return store.size() ;
		} // DataSize
		
		void Readfile( string file_name ) {
				int i = 1 ;
				int size = 1000 ;
				char * line  = new char[size] ; // 讀垃圾
				char * testinform = new char[size] ;
				inform tempinform ;
				FILE * file ;
				string tempfile_name = file_name ;
			    tempfile_name = "input" + file_name + ".txt" ;
				file = fopen( tempfile_name.c_str(), "r" ) ;
				if ( file == NULL )
				    cout << "### " << tempfile_name << " does not exist! ###" << endl ;
			    else {
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
			    	fscanf( file, "%[^\n]%*c", line ) ;
		    	
					while ( fscanf( file, "%s", testinform ) != EOF ) {
						tempinform.schOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.schName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depOid = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.depName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.day = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.dayName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.level = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.levelName = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.studentNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.teacherNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.graduator = atoi(testinform) ;
						fscanf( file, "%s", testinform ) ;
						tempinform.countryNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.country = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.typeNum = testinform ;
						fscanf( file, "%s", testinform ) ;
						tempinform.type = testinform ;
						
						tempinform.list = i ;
						i++ ;
					
						store.push_back( tempinform ) ;
					} // while
				
					delete [] line ;
					delete [] testinform ;
					fclose( file ) ;
				} // else
			
			} // Readfile
			
			void test () {
				int site = 0, size = sorted.size() ;
				for ( ; site < size ; site++ ) {
					cout << sorted.at(site).list << "\t" << sorted.at(site).graduator << endl ;
				} // for
			} // test
			
			// **********************************任務二*********************************************** 
			
			void compareMin ( int now ) {		
				int parent = ( now-1 ) / 2 ;
				bool judge = false ;
				if ( sorted.at(now).graduator < sorted.at(parent).graduator ) {
					swap( sorted.at(now), sorted.at(parent) ) ;
					judge = true ;
					now = parent ;
					parent = ( parent-1 ) / 2 ;
					parent = ( parent-1 ) / 2 ;
				} // if
				
				if ( judge == false ) {
					parent = ( parent-1 ) / 2 ;
					while ( now >= 7 ) {
						if ( sorted.at(now).graduator > sorted.at(parent).graduator ) {
							swap( sorted.at(now), sorted.at(parent) ) ;
							now = parent ;
							parent = ( parent-1 ) / 2 ; // 隔代檢查
							parent = ( parent-1 ) / 2 ;
						} // if
						else {
							break ;
						} // else
					
					} // while
				} // if
				else {
					while ( now >= 3 ) {
						if ( sorted.at(now).graduator < sorted.at(parent).graduator ) {
							swap( sorted.at(now), sorted.at(parent) ) ;
							now = parent ;
							parent = ( parent-1 ) / 2 ; // 隔代檢查
							parent = ( parent-1 ) / 2 ;
						} // if
						else {
							break ;
						} // else
					
					} // while
				} // else
				
				
			} // compareMin
			
			void compareMax ( int now ) {
				int parent = ( now-1 ) / 2 ;
				bool judge = false ;
				if ( sorted.at(now).graduator > sorted.at(parent).graduator ) {
					swap( sorted.at(now), sorted.at(parent) ) ;
					judge = true ;
					now = parent ;
					parent = ( parent-1 ) / 2 ;
					parent = ( parent-1 ) / 2 ;
				} // if
				
				if ( judge == false ) {
					parent = ( parent-1 ) / 2 ;
					while ( now >= 3 ) {
						if ( sorted.at(now).graduator < sorted.at(parent).graduator ) {
							swap( sorted.at(now), sorted.at(parent) ) ;
							now = parent ;
							parent = ( parent-1 ) / 2 ; // 隔代檢查
							parent = ( parent-1 ) / 2 ;
						} // if
						else {
							break ;
						} // else
					
					} // while
				} // if
				else {
					while ( now >= 7 ) {
						if ( sorted.at(now).graduator > sorted.at(parent).graduator ) {
							swap( sorted.at(now), sorted.at(parent) ) ;
							now = parent ;
							parent = ( parent-1 ) / 2 ; // 隔代檢查
							parent = ( parent-1 ) / 2 ;
						} // if
						else {
							break ;
						} // else
					
					} // while
				} // else
			} // compareMax
			
			
			void sorting () {
				// *******************先放第一筆資料**************************
				sortinform tempinform ;
				tempinform.graduator = store.at(0).graduator ;
				tempinform.list = store.at(0).list ;
				sorted.push_back( tempinform ) ; 
				
				// *******************邊放邊比較******************************
				
				int num = 1 ;
				while ( num < DataSize() ) {
					tempinform.graduator = store.at(num).graduator ;
					tempinform.list = store.at(num).list ;
					sorted.push_back( tempinform ) ;
					
					int point = num ;
					int count = 0 ;
					while ( point > 0 ) {
						point = ( point-1 ) / 2 ;
						count++ ; // 算在第幾層 
					} // while
					
					if ( count % 2 == 0 ) {
						compareMax( num ) ;	// min到max 
					} // if
					else {
						compareMin( num ) ; // max到min
					} // else
					
					
					
					
					num++ ; 
				} // while
				
				num-- ; // bottom位置
				 
				// *******************找最左邊節點***************************** 
				
				int point = num ;
				int count = 0 ;
				while ( point > 0 ) {
					point = ( point-1 ) / 2 ;
					count++ ; // 算在第幾層 
				} // while
				
				while ( count > 0 ) {
					point = point * 2 + 1 ;
					count-- ;
				} // while	 
				 
				// *******************印出數據********************************** 
				
				cout << "root: [" << sorted.at(0).list << "] " << sorted.at(0).graduator << "\n" ;
				cout << "bottom: [" << sorted.at(num).list << "] " << sorted.at(num).graduator << "\n" ;
				cout << "leftmost bottom: [" << sorted.at(point).list << "] " << sorted.at(point).graduator << "\n" ;	
				
			} // sorting
			
	
	
	
};



int main(int argc, char** argv) {
	int num = 0 ;
	bool done = false ;
	string file_name ;
	Job1 heap1 ;
	Job2 heap2 ;
	do {
		cout << "**** Heap Construction *****" << endl ;
		cout << "* 0. QUIT                  *" << endl ;
		cout << "* 1. Build a min heap      *" << endl ;
		cout << "* 2. Build a min-max heap  *" << endl ;
		cout << "****************************" << endl ;
		cout << "Input a choice(0, 1, 2): " ;
		
		cin >> num ;
		if ( num == 0 )
		    done = true ;
		else if ( num == 1 ) {
			cout << "Input a file number ([0] Quit): " ;
			cin >> file_name ;
			heap1.Readfile( file_name ) ;
			cout << "<min heap>" << endl ;
			heap1.sorting() ;
			heap1.Init() ;
		} // else if
		else if ( num == 2 ) {
			cout << "Input a file number ([0] Quit): " ;
			cin >> file_name ;
			heap2.Readfile( file_name ) ;
			cout << "<min-max heap>" << endl ;
			heap2.sorting() ;
			heap2.test() ;
			heap2.Init() ;
		} // esle if
		
	
	
	
	
	
	
	
	
	
		
	} while( !done ) ;
		
} // main
