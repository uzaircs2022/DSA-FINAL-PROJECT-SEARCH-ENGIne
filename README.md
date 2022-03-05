# DSA-FINAL-PROJECT-SEARCH-ENGIne
A code of a search engine of movies 

#include <iostream>
#include <fstream>

using namespace std;

class node
{
private:
    string ID;
    float rating;
    int votes;
    float MovieRating;
    node *next;
public:
    // Constructor For Node Class
    node()
    {
        votes = 0;
        rating = 0;
        MovieRating = 0;
        ID = nullptr;
        next=NULL;
    }

    // PARAMETERIZED CONSTRUCTOR

    node(string a,float b,int c,float d)
    {
        votes = c;
        rating = b;
        ID = a;
        MovieRating = d;
        next=NULL;
    }

    //ALL GETTER AND SETTERS FOR THE ATTRIBUTES
    void setID(string a)
    {
        ID = a;
    }
    void setrating(float a)
    {
        rating = a;
    }
    void setvotes(int a)
    {
        votes = a;
    }
    void setMovieRating(float f)
    {
        MovieRating = f;
    }
    void setnext(node* b)
    {
        next = b;
    }
    string getID()
    {
        return ID;
    }
    float getrating()
    {
        return rating;
    }
    int getvotes()
    {
        return votes;
    }
    float getMovieRating()
    {
        return MovieRating;
    }
    node* getnext()
    {
        return next;
    }
}; // end of first class



class LinkedList
{
private:
    // ATTRIBUTES OF LINKEDLIST CLASS
    long long SumOfVotes = 0;
    float SumOfRating = 0;
    long long ArrayToStoreSize[101] = {0};
    node* start[101];
    string IdForMostPopularMovie;
    string IdOfTheMovieHavingHighesVotes;
    string IdOfTheMovieHavingLowestVotes;
    int HighestVotes = 0;
    int LowestVotes = 5000;
    float RatingOfLeastPopularMovie = 10;
    float RatingOfMostPopularMovie = 0;
    string IdForLeastPopularMovie;
    long long CounterForAllMovies = 0;
    float RatingChecker;
public:
    LinkedList()
    {
        for(int i=0; i<101 ; i++ )
        {
            start[i]=NULL;
        }
        load();
    }

    // ALL FUNCTIONS FOR LINKEDLIST CLASS

    // Start Of HASH FUNCTION
    int hashfunction(long long key)
    {
        return key%10;
    } // END OF HASH FUNCTION

    //ADDITION FUNCTION
    void  addition(string a,float b,int c,float d,int index)
    {
        long long x;
        node* temp= new node(a,b,c,d);
        node* temp2= start[index];
        start[index] = temp;
        temp->setnext(temp2);
    }// END OF ADDITION FUNCTION


    // Rating Function
    float RatingOfMovie(float rating,int votes)
    {
        float a,b,c,d,e,f;
        a = votes+1000;
        b = votes / a;
        c = b*rating;
        d = 1000/a;
        e = d*7;
        f = c + e;
        return f;
    } // End of RAting Function


    // FUNCTION TO CHECK MOST POPULAR MOVIE
    void PopularMovie()
    {
        cout << "The Most Popular Movie has Id Number = " << IdForMostPopularMovie << endl;
        cout << "The Most Popular Movie has Rating = " << RatingOfMostPopularMovie << endl;
        cout << "______________________________________" << endl;

    } // END OF POPULAR MOVIE FUNCION

    // FUNCTION TO CHECK LEAST POPULAR MOVIE
    void LeastMovie()
    {
        cout << "The Least Popular Movie has Id Number = " << IdForLeastPopularMovie << endl;
        cout << "The Least Popular Movie has Rating = " << RatingOfLeastPopularMovie << endl;
        cout << "______________________________________" << endl;

    } // END OF LEAST MOVIE FUNCION


    //Function to check movie of equal rating
    void EqualRating()
    {
        int ValueUseToDisplay_j = 0,ValueUseToDisplay_k = 0;    // using for display purpose
        for(int i=1 ; i<=100 ; i++)
        {
            if(ValueUseToDisplay_k == 9)    // using for display purpose
            {
                ValueUseToDisplay_k = -1;
                ValueUseToDisplay_j ++ ;
            }
            cout << "Movies Have Rating " << ValueUseToDisplay_j << "." << ValueUseToDisplay_k+1 <<  " = " << ArrayToStoreSize[i] << endl;
            cout << "______________________________________" << endl;

            ValueUseToDisplay_k++;
        }
    }
    // End of Equal rating function

    //Function to calculate number of movies
    void TotalMovies()
    {
        cout << "Total number Of movies are " << CounterForAllMovies << endl;
        cout << "______________________________________" << endl;

    }
    //End Of TotalMovies Function

    //Function to display movie Having Lowest Votes
    void Lowest_votes()
    {
        cout << " Id of the Movie Having Lowest votes is  " << IdOfTheMovieHavingLowestVotes << endl;
        cout << "Votes of the movie are " << LowestVotes << endl;
        cout << "______________________________________" << endl;


    }
    //End of Lowest function

    //Function to display movie Having Highest Votes
    void Highest_votes()
    {
        cout << " Id of the Movie Having Highest votes is  " << IdOfTheMovieHavingHighesVotes << endl;
        cout << "Votes of the movie are " << HighestVotes << endl;
        cout << "______________________________________" << endl;


    }
    //End of Highest function

    //Function to get index
    int GetIndex(float a)
    {
        int check;
        check = a*10;
        return check;
    }
    // End of Get Index

    //Function to display any node
    void Display(node* x)
    {
        cout << "ID = " << x->getID() << endl;
        cout << "Votes = " << x->getvotes() << endl;
        cout << "Rating = " << x->getMovieRating() << endl;
    }
    // END OF Display FUNCTION

    //Function for top Five movies
    void TopFive()
    {
        float value = 10;
        string IdChecker = "0000000" ;
        cout << "Top 5 Movies are :" << endl;
        cout << "______________________________________" << endl;
        float RateChecker = 0;
        float CheckerOfTopLinkedList = RatingOfMostPopularMovie;
        int CheckerOfTopLinkedList1 = CheckerOfTopLinkedList*10;
        node*temp = start[CheckerOfTopLinkedList1];
        node*Top[5];
        for(int i=0 ; i<=4 ; i++)
        {
            temp = start[CheckerOfTopLinkedList1];
            while(temp != nullptr)
            {
                if(temp->getMovieRating() > RateChecker && temp->getID() != IdChecker && temp->getMovieRating()<= value )
                {
                    RateChecker = temp->getMovieRating();
                    Top[i] = temp;
                }
                temp = temp->getnext();
            }
            value = Top[i]->getMovieRating();
            IdChecker = Top[i]->getID();
            RateChecker = 0;
            cout <<  "No " << i+1 << endl;
            Display(Top[i]);
            cout << "______________________________________" << endl;

        }

    }
    // END OF TopFIVE FUNCTION



    //Function to compute average number of votes
    void AverageVotes()
    {
        cout << "Average votes = " << SumOfVotes/CounterForAllMovies << endl;
        cout << "______________________________________" << endl;


    }
    //End of Average Votes

    //Function to compute average number of rating
    void AverageRating()
    {
        cout << "Average Rating = " << SumOfRating/CounterForAllMovies << endl;
        cout << "______________________________________" << endl;


    }
    //End of Average Rating

    //Function to compute the movie at specified index
    void MoviesAtSpecified(float Rating)
    {
        int checker;
        checker = GetIndex(Rating);
        cout << "Number Of movies required at specified rating are = " << ArrayToStoreSize[checker] << endl;
        cout << "______________________________________" << endl;


    }
    //End Of MoviesAtSpecified

    // FUNCTION TO LOAD ALL DATA
    void load()
    {
        int ValueForHash;
        string ReceiverForSerialNumber;
        int ReceiverForVotes;
        float ReceiverForRating;
        ifstream ObjectOfStreamClass;
        ObjectOfStreamClass.open("data.txt");
        while(ObjectOfStreamClass.eof()==0)
        {
            ObjectOfStreamClass >> ReceiverForSerialNumber;
            ObjectOfStreamClass >> ReceiverForRating;
            ObjectOfStreamClass >> ReceiverForVotes;
            RatingChecker = RatingOfMovie(ReceiverForRating,ReceiverForVotes);
            if(RatingChecker > RatingOfMostPopularMovie)
            {
                RatingOfMostPopularMovie = RatingChecker;
                IdForMostPopularMovie = ReceiverForSerialNumber;
            }

            else if(RatingChecker < RatingOfLeastPopularMovie)
            {
                RatingOfLeastPopularMovie =  RatingChecker;
                IdForLeastPopularMovie = ReceiverForSerialNumber;
            }
            // condition for the movie having highest votes
            if(HighestVotes < ReceiverForVotes)
            {
                HighestVotes = ReceiverForVotes;
                IdOfTheMovieHavingHighesVotes = ReceiverForSerialNumber;
            }
            else if(LowestVotes > ReceiverForVotes)
            {
                LowestVotes = ReceiverForVotes;
                IdOfTheMovieHavingLowestVotes = ReceiverForSerialNumber;
            }
            ValueForHash = GetIndex(RatingChecker);
            ArrayToStoreSize[ValueForHash]++;
            CounterForAllMovies++;
            SumOfRating = SumOfRating + RatingChecker;
            SumOfVotes = SumOfVotes + ReceiverForVotes;
            addition(ReceiverForSerialNumber,ReceiverForRating,ReceiverForVotes,RatingChecker,ValueForHash);
        }
    }  // END OF LOAD DATA FUNCTION

};

// END OF LINKEDLIST CLASS


int main()
{
    // Object of our main class functions
    LinkedList ObjectOfLinkedListClass;
    char ChoiceToExitLoop;
    int ChoiceOfMenu;

    //Do-While loop
    do
    {
        cout << "====================================" << endl;
        cout << "Search Engine For the Data Of Movies" << endl;
        cout << "====================================" << endl;
        //Main Menu
        cout << "1.  Most Popular Movie" << endl;
        cout << "2.  Least Popular Movie" << endl;
        cout << "3.  Movies Having Equal Rating" << endl;
        cout << "4.  Top Five Movies" << endl;
        cout << "5.  Movie Having Highest Votes" << endl;
        cout << "6.  Movie Having Lowest Votes" << endl;
        cout << "7.  Total Number Of Movies" << endl;
        cout << "8.  Average Number Of votes" << endl;
        cout << "9.  Average Number Of Rating" << endl;
        cout << "10. Number Of Movies Of specified rating" << endl;
        cout << "______________________________________" << endl;
        cin >> ChoiceOfMenu;
        cout << "______________________________________" << endl;

        // Switch statement
        switch(ChoiceOfMenu)
        {
        case 1:
            ObjectOfLinkedListClass.PopularMovie();
            break;
        case 2:
            ObjectOfLinkedListClass.LeastMovie();
            break;
        case 3:
            ObjectOfLinkedListClass.EqualRating();
            break;
        case 4:
            ObjectOfLinkedListClass.TopFive();
            break;
        case 5:
            ObjectOfLinkedListClass.Highest_votes();
            break;
        case 6:
            ObjectOfLinkedListClass.Lowest_votes();
            break;
        case 7:
            ObjectOfLinkedListClass.TotalMovies();
            break;
        case 8:
            ObjectOfLinkedListClass.AverageVotes();
            break;
        case 9:
            ObjectOfLinkedListClass.AverageRating();
            break;
        case 10:
        {
            float answer;
            cout << "Enter the Rating of the movie you desired " << endl;
            cin >> answer;
            ObjectOfLinkedListClass.MoviesAtSpecified(answer);
            break;
        }
        default:
            cout << "Invalid Option" << endl;
            break;
        }

        cout << "Do You Want to Continue--- (y/n)--  " << endl;
        cout << "______________________________________" << endl;
        cin >> ChoiceToExitLoop;
        cout << "\n____________________________________\n" << endl;
    }
    while(ChoiceToExitLoop == 'y');

    // End Of While Loop

    return 0;
}
