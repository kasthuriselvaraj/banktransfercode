import java.sql.*;
import java.util.Scanner;
public class BankTransaction
{
       public static void main (String args []) throws Exception
       {
             Scanner s = new Scanner (System.in);
             System.out.println ("Enter the Source account number :");
             int saccno = s.nextInt ();
             System.out.println ("Enter the Destination account number :"); 
             int daccno = s.nextInt ();
             System.out.println ("Enter the amount to transfer :");
             int amnt = s.nextInt ();
             Class.forName ("oracle.jdbc.driver.OracleDriver :");
             Connection cn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:orcl", "god", "12345");
             Statement st = cn.createStatement ();
             cn.setAutoCommit (false);
             ResultSet rs = st.executeQuery ("select avail_balance from account_balance where account_number="+saccno);
             rs.next ();
             int abal = rs.getInt (1);
             if (abal>amnt)
            {
                 int upd = st.executeUpdate ("update account_balance"+amnt+ " account_number="+saccno);
                 int upd1 = st.executeUpdate ("update account_balance"+amnt+ " account_number="+daccno);
                 if (upd==1 && upd1==1)
                 {
                     cn.commit ();
                     System.out.printl(amnt+" balance is successfully Transferred:*******");
                 }
                 else
                 {
                      cn.rollback ();
                      System.out.println ("rollback");
                 }
            }
            else
            {
                System.out.println ("There is no sufficient balance");
            }
        }
}



![image](https://user-images.githubusercontent.com/51279124/89650637-9aeaac00-d877-11ea-91f4-7fba500714df.png)
![image](https://user-images.githubusercontent.com/51279124/89650678-a50caa80-d877-11ea-97a8-7fdd9561c6bd.png)




