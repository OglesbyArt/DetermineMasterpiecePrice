DetermineMasterpiecePrice
=========================
import java.util.*;

public class DetermineMasterpiecePrice
{

private String artistFirstName;
private String artistLastName;
private String titleOfWork;
private String classification;
//private date dateOfWork;
private double height;
private double width;
private String medium;
private String subject;
private double suggestedMaximumPurchasePrice;



    //Desc: constructor for DetermineOtherWorkPrice
	//Post: allows class to set the value of all Painting fields 
    // in a record
    public DetermineMasterpiecePrice(String fname, String lname, String work, String clas, double h,double w, String med, String sub, double max)
    {
		artistFirstName=fname;
		artistLastName=lname;
		titleOfWork=work;
	//	dateOfWork=dwork
		classification=clas;
		height=h;
		width=w;
		medium=med;
		subject=sub;
		suggestedMaximumPurchasePrice=max;
    }




    //Desc: Looks through the bought file for paintings by the same artist
    //and computes the coefficient of similarity for that painting. 
    //It will return the purchase price for the painting with the 
    //highest coefficient of similarity
    //Pre: There must be another painting by the same artist in 
    //the painting file
    //Return: The price of the painting with the highest coefficient
    //of similarity
    public static double findLargestCoefficientofSimilarity()
    {

    	double coeff=0;
    	double dummycoeff=0;
    	int score1=0;
    	int score2=0;
    	double largerarea=0;
    	double smallerArea=0;
    	double suggestMaxPrice=0;

       // create  determineMostSimilarWork object

     /*   loop through array for bought paintings objects
        {
        	find(artistname)
        	score1=computeScore(getmedium(), medium)
    		score2=computeScore(getsubject(), subject)
        	smallerArea=width*height 
        	largerArea=getWidth()*getHeight() 
    		largerarea=compareReturnLarger(largerarea, smallerArea)
    		smallerArea=compareReturnSmaller(largerarea, smallerArea)
			dummycoeff=computeCoefficientofSimilarity(score1, 
                        smallerArea, largerarea)
			if (coeff<dummycoeff)
			{
				coeff=dummycoeff
				suggestMaxPrice=maxpurchaseprice
			}
    	}*/
    	return suggestMaxPrice;
    }
    
    //Desc: calculate the price for the Masterpiece the user wants to buy
    //Pre: there must be a most similar work and that work must have a an 
    //auction purchase price, the user must have entered the 
    // date of the work correctly
    //Return: the price of the Masterpiece 
    public static double calculateMasterpiecePrice()
    {
    	double auctionPurchasePrice=findLargestCoefficientofSimilarity();
    	int currentYear=2014;//getDate()
    	int auctionYear =2000;// dateOfWork
    	return auctionPurchasePrice;//*(8.5)^((1/auctionYear)-currentYear) + 1;
    }
}
    
