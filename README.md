# Task3
Создать проект, позволяющий из одного текстового файла,  содержащего несколько строк (тип String) заранее подготовленного текста  на русском языке (Пушкин, Лермонтов или другой российсмки классик на  Ваш вкус), построчно переписать в другой текстовый файл слова  начинающиеся с согласных букв

package project10;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.util.ArrayList;

public class KlassFile12 {
	public static void main(String[] args) throws IOException {
		BufferedReader in = null;
		PrintWriter out = null;
		int i = 0;
		try {
			in = new BufferedReader( new InputStreamReader( new FileInputStream(GetFileByName("Task3Input.txt")),"cp1251"));
			out = new PrintWriter(GetFileByName("Task3Output.txt"), "cp1251");
			String line;
			while ((line = in.readLine()) != null) {
				i++;
				for (String string : GetWords(line/*.replaceAll(",|.", "")*/)) {
					System.out.println(i+": "+string);
					out.println(i+": "+string);
				}
				line = in.readLine();
			}
		} 
		catch (Exception e) {
			System.out.println("Error: " + e.getMessage());
		}
		finally {
			in.close();
			out.flush();
			out.close();
		}
	}

	private static String DirPath = "C:\\Test\\%s";
	public static File GetFileByName(String filename) throws IOException {
		 File f1=new File(String.format(DirPath, filename));
		 return f1;
	}

	private static ArrayList<String> GetWords(String inStr)
	{
		ArrayList<String> res = new ArrayList<String>();
		for (String string : inStr.split(" ")) {
			if (StartsWithСonsonant(string)) {
				res.add(string);
			}
		}		
		return res;
	}
	private static String ConsonantList = "бвгджзйклмнпрстфхцчшщ";
	private static boolean StartsWithСonsonant(String inStr)
	{
		return ConsonantList.contains(inStr.subSequence(0, 1));
	}

}
