#include "helpers.h"
#include <math.h>
#include <stdio.h>
// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0 ; i < height ; i++)
    {
        for (int j = 0 ; j < width ; j++)
        {
            double average = (image[i][j].rgbtRed + image[i][j].rgbtGreen + image[i][j].rgbtBlue) / 3.0;
            //  printf("%f",round(average));
            image[i][j].rgbtRed = round(average);
            image[i][j].rgbtGreen = round(average);
            image[i][j].rgbtBlue = round(average);
        }
    }
    return;
}

// Convert image to sepia
void sepia(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0 ; i < height ; i++)
    {
        for (int j = 0 ; j < width ; j++)
        {
            int originalRed = image[i][j].rgbtRed;
            int originalGreen = image[i][j].rgbtGreen;
            int originalBlue = image[i][j].rgbtBlue;
            double sepiaRed = .393 * originalRed + .769 * originalGreen + .189 * originalBlue;
            double sepiaGreen = .349 * originalRed + .686 * originalGreen + .168 * originalBlue;
            double sepiaBlue = .272 * originalRed + .534 * originalGreen + .131 * originalBlue;
             
            if (sepiaRed < 0) 
            {
                sepiaRed = 0;
            }
            else if (sepiaRed > 255) 
            {
                sepiaRed = 255;
            }
            
            if (sepiaGreen < 0) 
            {
                sepiaGreen = 0;
            }
            else if (sepiaGreen  > 255) 
            {
                sepiaGreen = 255;
            }
            if (sepiaBlue < 0)  
            {
                sepiaBlue = 0;
            }
            else if (sepiaBlue  > 255)  
            {
                sepiaBlue = 255;
            }
            
            image[i][j].rgbtRed = round(sepiaRed);
            image[i][j].rgbtGreen = round(sepiaGreen);
            image[i][j].rgbtBlue = round(sepiaBlue);
        }
    }    
    return;
}

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    
    for (int i = 0 ; i < height ; i++)
    {   
        int newRed[width];
        int newGreen[width];
        int newBlue[width];
        for (int j = 0 ; j < width ; j++)
        {
            newRed[width - j - 1] = image[i][j].rgbtRed;
            newGreen[width - j - 1] = image[i][j].rgbtGreen;
            newBlue[width - j - 1] = image[i][j].rgbtBlue;
        }
        for (int j = 0 ; j < width ; j++)
        {
            image[i][j].rgbtRed = newRed[j];
            image[i][j].rgbtGreen = newGreen[j];
            image[i][j].rgbtBlue = newBlue[j];
        }
    }
    return;
}

// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    RGBTRIPLE new[height][width];

    double average_red = 0, average_green = 0, average_blue = 0;
    int count = 0;

    for (int i = 0 ; i < height ; i++)
    {
        for (int j = 0 ; j  < width ; j++)
        {    

            //for pixel in a blur box
            for (int box_y = i - 1; box_y <= i + 1; box_y ++)
            {
                for (int box_x = j - 1; box_x <= j + 1; box_x ++)
                {
                    //when at edge, count these pixels as 0, dont add count
                    if (box_y < 0 || box_y == height || box_x < 0 || box_x == width)
                    {
                        continue;
                    }
                    //count how many pixels in a box to add
                    count++; 

                    average_red += image[box_y][box_x].rgbtRed;
                    average_green += image[box_y][box_x].rgbtGreen;
                    average_blue += image[box_y][box_x].rgbtBlue;
                }
            }
            // printf("%i",count);
            //store the new average to the a list
            int red = round(average_red / count) ;
            int green = round(average_green / count);
            int blue = round(average_blue / count);



            image[i][j].rgbtRed = red;
            image[i][j].rgbtGreen = green;
            image[i][j].rgbtBlue = blue;


            average_red = 0;
            average_blue = 0;
            average_green = 0;
            count = 0;
        }
    }

    return;
}
