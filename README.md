import java.util.*;
public class Main
{
    static ArrayList<Integer> playerPositions=new ArrayList<>();
     static ArrayList<Integer> cpuPositions=new ArrayList<>();
	public static void main(String[] args) {
		char[][] board={{' ','|',' ','|',' '},
		                 {'-','+','-','+','-'},
		                 {' ','|',' ','|',' '},
		                 {'-','+','-','+','-'},
		                 {' ','|',' ','|',' '}};
		printGameBoard(board);
		
		while(true)
		{
		   Scanner sc=new Scanner(System.in);
		   System.out.println("Enter your position from 1 to 9:");
		   int playerPosition=sc.nextInt();
		   while(playerPositions.contains(playerPosition) || cpuPositions.contains(playerPosition))
		   {
		       System.out.println("position already filled please choose another position:");
		        playerPosition=sc.nextInt();
		   }
	       placingInPos(board,playerPosition,"player");
	       String res=checkForWinner();
	       if(res.length()>0)
	       {
	           System.out.println(res);
	           break;
	       }
	       Random rand=new Random();
	       int cpuPosition=rand.nextInt(9)+1;
	       while(playerPositions.contains(cpuPosition) || cpuPositions.contains(cpuPosition))
	       {
	           cpuPosition=rand.nextInt(9)+1;
	       }
		   printGameBoard(board);
		   placingInPos(board,cpuPosition,"cpu");
		   System.out.println("cpu's turn:");
		   printGameBoard(board);
		   res=checkForWinner();
		   if(res.length()>0)
	       {
	           System.out.println(res);
	           break;
	       }
		}
	}
	public static void printGameBoard(char[][] board)
	{
	    for(char[] c:board)
		{
		    for(char row:c)
		    {
		        System.out.print(row);
		    }
		    System.out.println();
		}
	}
	public static void placingInPos(char[][] board,int position,String user)
	{
	    char symbol=' ';
	    if(user.equals("player"))
	    {
	        symbol='X';
	        playerPositions.add(position);
	    }
	    else if(user.equals("cpu"))
	    {
	        symbol='O';
	        cpuPositions.add(position);
	    }
	    switch(position)
		{
		    case 1:
		        board[0][0]=symbol;
		        break;
		    case 2:
		        board[0][2]=symbol;
		        break;
		    case 3:
		        board[0][4]=symbol;
		        break;
		    case 4:
		        board[2][0]=symbol;
		        break;
		    case 5:
		        board[2][2]=symbol;
		        break;
		    case 6:
		        board[2][4]=symbol;
		        break;
		    case 7:
		        board[4][0]=symbol;
		        break;
		    case 8:
		        board[4][2]=symbol;
		        break;
		    case 9:
		        board[4][4]=symbol;
		        break;
		   default:
		        break;
		}
	}
	public static String checkForWinner()
	{
	    List topRow=Arrays.asList(1,2,3);
	    List midRow=Arrays.asList(4,5,6);
	    List bottomRow=Arrays.asList(7,8,9);
	    List topCol=Arrays.asList(1,4,7);
	    List midCol=Arrays.asList(2,5,8);
	    List bottomCol=Arrays.asList(3,6,9);
	    List cross1=Arrays.asList(1,5,9);
	    List cross2=Arrays.asList(7,5,3);
	    List<List> checkWinConditions=new ArrayList<>();
	    checkWinConditions.add(topRow);
	    checkWinConditions.add(midRow);
	    checkWinConditions.add(bottomRow);
	    checkWinConditions.add(topCol);
	    checkWinConditions.add(midCol);
	    checkWinConditions.add(bottomCol);
	    checkWinConditions.add(cross1);
	    checkWinConditions.add(cross2);
	    for(List l:checkWinConditions)
	    {
	    if(playerPositions.containsAll(l))
	       return "Hurray!Congratulations you won";
	   else if(cpuPositions.containsAll(l))
	       return "Oops!You lost Better luck next time";
	   else if(playerPositions.size()+cpuPositions.size()==9)
	       return "Tie";
	    }
	    return "";
	}
}
