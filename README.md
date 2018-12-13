/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package guessthemovie;

import java.io.File;
import java.io.FileNotFoundException;
import static java.lang.System.out;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Scanner;

/**
 *
 * @author nguyenjoh
 */
public class GuesstheMovie {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) throws FileNotFoundException {
      System.out.println("The rules are simple, the computer randomly ");
      System.out.println("picks a movie title, and shows you how many letters"); 
      System.out.println("it's made up of. Your goal is to try to figure out ");
      System.out.println("the movie by guessing one letter at a time.");
        
        List<String> words = new ArrayList<>();
        Scanner scan = new Scanner(new File("movies.txt"));
      
        while (scan.hasNext()){
            String str = scan.nextLine();
            words.add(str);
            } 
        int random = (int)(Math.random() * 29  + 1);
        
        String movie = (words.get(random));
        
        String result = movie.replaceAll("[A-Za-z]", "_ ");
        String [] splits = new String[movie.length()];
        for (int i = 0; i < movie.length(); i++) {
            splits[i] = "-";
        }
        //String [] splits = movie.split("");
        
        System.out.println(result);
        System.out.println("Start the game by pressing space then enter two times!");
        
        //System.out.println(Arrays.toString(splits));
        HashSet<Character> usedLetters = new HashSet<>();
        String currentWord = "";        
        Scanner userInput = new Scanner(System.in);
        String guess = userInput.nextLine();
        //int count = 0;
        int numGuess = 0;
        int lastNum = 0;
        
        while(true){
            System.out.println("Movie is:");
            currentWord = "";
            for(int i = 0; i < splits.length; i++) {
                //count++;
                out.print(splits[i]);
            }
            out.println("Guess a letter");
            guess = userInput.nextLine(); 
            if(guess.length() != 1) {
                out.println("Invalid guess try again");
            }
            else if (usedLetters.contains(guess.charAt(0))) {
                out.println("Already guessed that try again");
            }        
            else if (!movie.contains(guess)) {
                usedLetters.add(guess.charAt(0));
                numGuess++;
                int guessLeft = (10 - numGuess);
                out.println("NOPE! " + guessLeft + " lives left");
                lastNum = guessLeft;
            }
            else if (movie.contains(guess)) {
            for(int i = 0; i < movie.length(); i++) 
            {
                if(movie.charAt(i) == guess.charAt(0)) 
                {
                  splits[i] = "" + guess.charAt(0);
                }
            currentWord += splits[i];
                    
                }
            } 
            int guessLeft = (10 - numGuess);
            if(guessLeft == 0)
                break;
            if(currentWord.equals(movie)) 
          break;
          }
        if(currentWord.equals(movie)) {
           out.println("GOOD JOB! the movie was " + currentWord);
        } else if (lastNum == 0) {
            out.println("YOURE OUT OF LIVES, YOU SUCK IT WAS OBVIOUSLY " + 
                    movie + " YOURE SO DUMB");
            
        }
    }
    }
