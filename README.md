/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */

/**
 *
 * @author katiejesperson
 */
 package oglesby;

import java.util.*;

import java.io.*;

class DetermineMasterpiecePrice {




    //Desc: constructor for DetermineMasterpiecePrice
     //Post: Creates a new DetermineMasterpiecePrice
    public DetermineMasterpiecePrice()
    {
        executeDetermineMasterpiecePrice();
    }

    //Desc: Executes the major methods that allow a user to buy a painting.
    //  First the user must input values, then the user will view the
    //  suggested price. If the user chooses by buy then the bought painting
    //  file will be updated, otherwise the user can go back to the main
    //  menu
    //Pre: The coefficient of similarity must not be zero, otherwise
    //  the user is not interested in buying the painting.
    //Post: The user will have viewed the suggested maximum price for
    //  the painting they want to buy. If they chose to buy it, the files are
    //  now updated accordingingly.
    public static void executeDetermineMasterpiecePrice()
    {
       BoughtPainting bp = new BoughtPainting();
        bp.setClassification("Masterpiece");
        bp.readInRecord();
        double area =bp.getHeight()*bp.getWidth();
        boolean choice=false;
        double suggestedMaximumPurchasePrice=calculateMasterpiecePrice(bp.getArtistLastName(), bp.getSubject(), bp.getMedium(),area, bp.getDateofWork() );
        if (suggestedMaximumPurchasePrice==0)
        {
            choice=false;
        }
        else choice = userBuyChoice(suggestedMaximumPurchasePrice);
        if ( choice)
        {
            bp.setSuggestedMaximumPurchasePrice(suggestedMaximumPurchasePrice);
            bp.addRecentlyBought();
            UserInterface.pressEnter();
        }
                
        else UserInterface.pressEnter();
    }

    //Desc: calculate the price for the Masterwork the user wants to buy
    //Pre: there must be a most similar work and that work must have a an
    //  auction purchase price, the user must have entered
    //  the date of the work correctly
    //Return: the price of the Masterwork
    public static double calculateMasterpiecePrice(String artistLastName, String subject, String medium, double area, Date dateOfWork)
    {

        DetermineMostSimilarWork ap = new DetermineMostSimilarWork();
        Date auctiondate;

    	double auctionPurchasePrice=ap.findPrice(artistLastName,  medium,subject, area);
        if (auctionPurchasePrice==0)
        {
            return 0;
        }

    	Date currentDate =new Date();
    	Calendar cal = Calendar.getInstance();


        auctiondate=ap.findDate(artistLastName,  medium, subject,  area);
        cal.setTime(auctiondate);
        int dateOfAuctionYear = cal.get(Calendar.YEAR);

        cal.setTime(currentDate);
        int currentDateYear = cal.get(Calendar.YEAR);



        double masterpiecePrice = auctionPurchasePrice* Math.pow((1+.085), currentDateYear-dateOfAuctionYear);

        return masterpiecePrice;


    }


    //Desc: display a value to the user and the user responds
    //  which is returned as a true or false value
    //Pre: the argument must be a double value
    //Return: a boolean value based on the user’s input
    public static boolean userBuyChoice(double d)
    {
    	System.out.println("The price is " +d +". Do you want to buy? y/n");
    	String choice=UserInterface.getString();
        while (!choice.equalsIgnoreCase("y")&&!choice.equalsIgnoreCase("n"))
        {
            System.out.println("Please enter the correct format, either y or n");
            System.out.println("The price is " +d +". Do you want to buy? y/n");
            choice=UserInterface.getString();
        }

        if (choice.equalsIgnoreCase("y")) return true;
        else return false;


    }

}
