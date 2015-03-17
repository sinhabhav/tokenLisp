










package Package1;

import java.io.*;

import java.util.*;

public class Class1 {
	public static void main(String args[] ) throws Exception {
		/* improvements needed : handle exception cases*/
		Scanner sc = new Scanner(System.in);

		while(sc.hasNext())
		{
			// else part will contain errors reporting
			String str = sc.nextLine();
			String function="";
			ArrayList<String> funcList = new ArrayList<String>();
			ArrayList<String> numList =new ArrayList<String>();
			int countFun =-1;
			int countNum=-1;
			int countBrac = 0;
			char ch;
			boolean flag=false;
			int len = str.length();
			for (int i=0;i<len;i++)
			{	
				ch=str.charAt(i);
				if(!(ch=='a'||ch=='d'||ch=='m'||ch=='l'||ch=='u'||ch=='('||ch==')'||(((int)(str.charAt(i)))>=48))||(((int)(str.charAt(i)))<=57))
				break;
				function="";
				if(str.charAt(i)=='(')
				{	
					if(i==0)
						flag=true;
					countBrac++;
					i++;
					function="";
					if(str.charAt(i)=='a'||str.charAt(i)=='m')
					{
						function =function+str.charAt(i)+"";
						i++;

						if(str.charAt(i)=='d'||str.charAt(i)=='u')
						{
							function +=str.charAt(i)+"";
							i++;
							if(str.charAt(i)=='d'||str.charAt(i)=='l')
							{
								function +=str.charAt(i)+"";
								if(function.equals("add")||function.equals("mul"))
								{
									funcList.add(function);
									countFun++;

								}
								else
									flag=false;
							}
							else
								flag=false;
						} 
					}

				}


				if(((int)(str.charAt(i)))>=48 && ((int)(str.charAt(i)))<=57)
				{

					numList.add(Character.toString(str.charAt(i)));
					countNum++;

				}
				if(str.charAt(i)==')')

				{
					countBrac--;
					String func = funcList.get(countFun);
					funcList.remove(countFun);
					countFun--;
					int a = Integer.parseInt(numList.get(countNum));
					numList.remove(countNum);
					countNum--;

					int b = Integer.parseInt(numList.get(countNum));
					numList.remove(countNum);
					countNum--;
					if(func.equals("add"))
					{
						int c = a+b; 
						numList.add(c+"");
						countNum++;
					}

					if(func.equals("mul"))
					{
						int c = a*b; 
						numList.add(c+"");
						countNum++;
					}
				}
				if(countBrac==0 && flag ==true)
				{
					System.out.println(numList.get(countNum));
					break;
				}
			}          
		}
		sc .close();
	}
}
