BoughtPainting
==============
package artpricingsystem;

import java.io.File;
import java.io.RandomAccessFile;
import java.util.Date;
import java.util.Scanner;

class BoughtPainting extends Painting 
{

protected double suggestedMaxPurchPrice; 
protected Date dateOfPurchase;
protected String nameOfSeller;
protected String addressOfSeller;
protected double actualPurchasePrice;
protected double targetSellingPrice;

    //Desc: constructor for BoughtPainting
    //Post: allow class to set the value of all Bought Painting fields in a record
    BoughtPainting(String fname, String lname, String work, Date dwork, 
    String clas, double h, double w, String med, String sub, double max, 
    Date d, String n, String a, double p, double t)
    {
            artistFirstName=fname;
            artistLastName=lname;
            titleOfWork=work;
            dateOfWork=dwork;
            classification=clas;
            height=h;
            width=w;
            medium=med;
            subject=sub;
            suggestedMaxPurchPrice=max;
            dateOfPurchase=d;
            nameOfSeller=n;
            addressOfSeller=a;
            actualPurchasePrice=p;
            targetSellingPrice=t;
    }
    //Desc: constructor for BoughtPainting
    //Post: allows class to set a new record for a Bought Painting
    BoughtPainting()
    {
    }

    //Desc: allows class to access the dateOfPurchase field in a record
    //Return: dateOfPurchase
    public Date getDateOfPurchase() 
    {
            return dateOfPurchase;
    }

    //Desc:allows class to set the value of the dateOfPurchase field in a record
    //Post: dateOfPurchase is set to d
    public void setDateOfPurchase(Date d) 
    {
            dateOfPurchase=d;
    }

    //Desc: allows class to access the nameOfSeller field in a record
    //Return: nameOfSeller
    public String getNameOfSeller() 
    {
            return nameOfSeller;
    }

    //Desc: allows class to set the value of the nameOfSeller field in a record
    //Post: nameOfSeller is set to n
    public void setNameOfSeller(String n)
    {
            nameOfSeller=n;
    }

    //Desc: allows class to access the addressOfSeller field in a record
    //Return: addressOfSeller
    public String getAddressOfSeller()
    {
            return addressOfSeller;
    }

    //Desc:allows class to set the value of the addressOfSeller field in a record
    //Post: addressOfSeller is set to a
    public void setAddressOfSeller(String a)
    {
            addressOfSeller=a;
    }

    //Desc: allows class to access the actualPurchasePrice field in a record
    //Return: actualPurchasePrice
    public double getActualPurchasePrice()
    {
            return actualPurchasePrice;
    }
    //Desc: allows class to set the value of the actualPurchasePrice 
//      field in a record
    //Post: actualPurchasePrice is set to p
    public void setActualPurchasePrice(Double p) 
    {
            actualPurchasePrice=p;
    }

    //Desc: allows class to access the targetSellingPrice field in a record
    //Return: targetSellingPrice
    public double getTargetSellingPrice()
    {
            return targetSellingPrice;
    }

    //Desc: allows class to set the value of the targetSellingPrice field
//      in a record
    //Post: targetSellingPrice is set to t
    public void setTargetSellingPrice(Double t)
    {
            targetSellingPrice=t;
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		dateOfPurchase field in the found object
    //Post: dateOfPurchase field is updated
    public void updateDateOfPurchase() //will this ever change?
    {
        System.out.println("Old Date of Purchase:" + dateOfPurchase);
        System.out.println("Please enter new Date of Purchase");
        Scanner input=new Scanner(System.in);
        String d=input.next();
        //dateOfPurchase=d; //convert string into a date
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		nameOfSeller field in the found object
    //Post: nameOfSeller field is updated
    public void updateNameOfSeller()
    {
        System.out.println("Old Name of Seller:" + nameOfSeller);
        System.out.println("Please enter new Name of Seller");
        Scanner input=new Scanner(System.in);
        while (input.hasNext())
            nameOfSeller+=input.next();
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		addressOfSeller field in the found object
    //Post: AddressOfSeller field is updated
    public void updateAddressOfSeller()
    {
        System.out.println("Old Address of Seller:" + addressOfSeller);
        System.out.println("Please enter new Address of Seller");
        Scanner input=new Scanner(System.in);
        while (input.hasNext())
            addressOfSeller+=input.next();
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		actualPurchasePrice field in the found object
    //Post: actualPurchasePrice field is updated
    public void updateActualPurchasePrice (String lname, String ptitle, double aprice)
    {
        System.out.println("Old Actual Purchase Price:" + actualPurchasePrice);
        System.out.println("Please enter new Actual Purchase Price");
        Scanner input=new Scanner(System.in);
        actualPurchasePrice=input.nextDouble();
    }
	
	//Desc: Finds the record the user wants to update and updates the 
	//		targetSellingPrice field in the found object
	//Post: targetSellingPrice field is updated
	public void updateTargetSellingPrice() //will this ever change?
	{
            System.out.println("Old Target Selling Price:" + targetSellingPrice);
            System.out.println("Please enter new Target Selling Price");
            Scanner input=new Scanner(System.in);
            targetSellingPrice=input.nextDouble();
	}
	
    //Desc: uses the last name of an artist and the title of work to find the
    // 		 Bought Painting object in the array 
    //Return: returns the found Artist object or null value if Artist not found
    public boolean find(String alastname, String title) //should only appear in painting
    {
        try
        {
            File paintingsFile = new File ("GalleryPaintings.dat");
            boolean found = false;		

            if (paintingsFile.exists ())
            {
                RandomAccessFile inFile = new RandomAccessFile (paintingsFile, "r");

                while (!found && (inFile.getFilePointer () != inFile.length ()))
                {
                    read (inFile);

                    if (artistLastName.equals(alastname) && titleOfWork.equals(title))
                        found = true;
                }
                  inFile.close();
            }
                return found;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: Investment.find () *****");
            System.out.println ("\t" + e);

            return false; //returns boolean right now, not artist
        }
    }
	//Desc: reads a file into the scanner, sets each field in the text file to 
	//		a field in a new Bought Painting object
	//Pre: file must exist
	public void read(RandomAccessFile fileName)
    {
        try
        {
            String  inputString = new String ();	// for storing artist record
            int	i = 0;		                // position in record
            inputString = fileName.readLine ();
            StringBuffer input = new StringBuffer ();	// for storing field within record
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistFirstName = input.toString ();
            i++;

            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistLastName = input.toString ();
            i++;

            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
             titleOfWork = input.toString ();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++; 
            }
             Date tempdow = new Date (input.toString ());
             dateOfWork = tempdow;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
             classification = input.toString ();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempheight = new Double (input.toString ());
            height = tempheight;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempwidth = new Double (input.toString ());
            height = tempwidth;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            medium = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            subject = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempmax = new Double (input.toString ());
            suggestedMaxPurchPrice = tempmax;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Date tempdop = new Date (input.toString ());
            dateOfPurchase = tempdop;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            nameOfSeller = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            addressOfSeller = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempactual = new Double (input.toString ());
            actualPurchasePrice = tempactual;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double temptarget = new Double (input.toString ());
            targetSellingPrice = temptarget;
            i++;           
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: Arist.read () *****");
            System.out.println ("\t" + e);
        }

      }
	//Desc: writes the variables dateOfPurchase, nameOfSeller, addressOfSeller, 
	//		actualPurchasePrice, and targetSellingPrice to a record in the file
	//Post: updates the specified file
	public void write(RandomAccessFile fileName)
	{
            try
            {
                fileName.writeChars(artistFirstName + "|" + artistLastName + 
                    "|" + titleOfWork+ "|" + dateOfWork + "|"+ 
                    classification + "|" + height + "|" + width + "|" + medium +
                    "|" + subject + "|" + suggestedMaxPurchPrice + "|" + 
                    dateOfPurchase + "|" + nameOfSeller + "|" + addressOfSeller+
                    "|" + actualPurchasePrice + "|" + targetSellingPrice + "\n");
            }
            catch (Exception e)
            {
                System.out.println ("***** Error: Artist.write () *****");
                System.out.println ("\t" + e);
            }
	}
    //Desc: writes the record back to the text file and prompts the 
    //      user the data has been saved
    //Post: changes the text file
    public void save()
    {
        try
        {
            File paintingsFile = new File ("GalleryPaintings.dat");	// file of artist
            File  temppaintingsFile = new File ("GaleryPaintings.tmp");	// temporary file for artist

            BoughtPainting tempBoughtPainting = new BoughtPainting ();	// record read, then written
            boolean found = false;		// terminates while-loop

            RandomAccessFile newFile = new RandomAccessFile (temppaintingsFile, "rw");

            if (!paintingsFile.exists ())
            {
              write(newFile);
            }
            else
            {
                RandomAccessFile oldFile = new RandomAccessFile (paintingsFile, "r");

                int comparePaintings; // to find correct place for the new investment

                while (oldFile.getFilePointer () != oldFile.length ()) //the pointer hasn't reached the end of the file
                {
                    tempBoughtPainting.read(oldFile); //read walks through each field in the record

                    if (artistLastName.equals(tempBoughtPainting.getArtistLastName())
                        && titleOfWork.equals(tempBoughtPainting.getTitleofWork()))
                        comparePaintings=1;
                    else comparePaintings=0;

                    if (comparePaintings ==1) 
                    {
                        write (newFile); //replaces old file record with new file record
                    } 
                    else
                    {
                      tempBoughtPainting.write (newFile); //writes to 2nd temp file
                    }
              }  // while

              //if (compareArist==0) write (newFile); // if never found in file, write to temp file

              oldFile.close ();

            }  // else

            newFile.close ();

            paintingsFile.delete ();
            temppaintingsFile.renameTo (paintingsFile);
            System.out.println("record saved");

          }
          catch (Exception e)
          {
              System.out.println ("***** Error: Artist.putRecord () *****");
              System.out.println ("\t" + e);
          }
    }
}
