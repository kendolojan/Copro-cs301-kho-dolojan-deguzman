using System;
using System.Data.SqlClient;

//INTERFACES
public interface IIsNewPlayer
{
    public void DisplayPlayerExperience();
    bool IsNew { get; set; }
}
public interface ICharacterCompanion
{
    public void DisplayCharacterCompanion(string SQLConnectionString, CharacterBiography myCharacterBio);
    public string Companion {  get; set; }
    public string CompanionElement { get; set; }
}
public interface ICharacterStats
{
    public void DisplayCharacterStats(string SQLConnectionString, CharacterBiography myCharacterBio);
    public int Strength { get; set;}
    public int Dexterity { get; set;}
    public int Intelligence { get; set;}
}
public interface ICharacterType
{
    void DisplayCharacterType(string SQLConnectionString, CharacterBiography myCharacterBio);
    string CharacterClass { get; set; }
    string CharacterElement { get; set; }
    string BodyArmor { get; set; }
    string LegArmor { get; set; }
    string Boots { get; set; }
}
public interface ICharacterDesign
{
    void DisplayCharacterDesign(string SQLConnectionString, CharacterBiography myCharacterBio);
    string HairStyle { get; set; }
    string HairColor { get; set; }
    string SkinColor { get; set; }
    string BodyType { get; set; }
    string ShirtColor { get; set; }
    string PantsColor { get; set; }
    string ShoeColor { get; set; }
    string Accessory { get; set; }
}

//ABSTRACT CLASS
public abstract class AB{
    
    //ABSTRACT METHODS
    public abstract void DisplayCharacterBiography(string SQLConnectionString, CharacterBiography myCharacterBio);
    public abstract string Username { get; set; }
    public abstract string Nickname { get; set; }
    public abstract string Gender { get; set; }
    public abstract string Pronouns { get; set; }
    public abstract string Bio { get; set; }

}

//INHERITANCE
public class CharacterBiography : AB
{
    private string username, nickname, gender, pronouns, bio;

    //CONSTRUCTOR
    public CharacterBiography()
    {
        Console.WriteLine("-- CHARACTER BIOGRAPHY --");
    }
    //METHOD OVERRIDING
    public override void DisplayCharacterBiography(string SQLConnectionString, CharacterBiography myCharacterBio)
    {
        try
        {
            SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();
            string username = myCharacterBio.username;
            string selectQuery = "SELECT * FROM dbo.Character WHERE username = '" + username + "'";
            SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

            SqlDataReader reader = selectCommand.ExecuteReader();

            while (reader.Read())
            {
                string DBusername = reader["username"].ToString();
                string DBnickname = reader["nickname"].ToString();
                string DBgender = reader["gender"].ToString();
                string DBpronouns = reader["pronouns"].ToString();
                string DBbio = reader["bio"].ToString();

                //Display the data inside the DB
                Console.WriteLine("\tUsername:\t" + DBusername);
                Console.WriteLine("\tNickname:\t" + DBnickname);
                Console.WriteLine("\tGender:\t\t" + DBgender);
                Console.WriteLine("\tPronouns:\t" + DBpronouns);
                Console.WriteLine("\tBio:\t\t" + DBbio);
                Console.WriteLine();
            }

            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }

    }

    public override string Username
    {
        get { return username; }
        set { this.username = value; }
    }
    public override string Nickname
    {
        get { return nickname; }
        set { this.nickname = value; }
    }
    public override string Gender
    {
        get { return gender; }
        set { this.gender = value; }
    }
    public override string Pronouns
    {
        get { return pronouns; }
        set { this.pronouns = value; }
    }
    public override string Bio
    {
        get { return bio; }
        set { this.bio = value; }
    }
}

//INHERITANCE
public class CharacterDesign : ICharacterDesign
{
    private string hair_style, hair_color, skin_color, body_type, shirt_color, pants_color, shoe_color, accessory;
    
    //CONSTRUCTOR
    public CharacterDesign()
    {
        Console.WriteLine("\n-- CHARACTER DESIGN --");
    }
    public void DisplayCharacterDesign(string SQLConnectionString, CharacterBiography myCharacterBio)
    {
        try
        {
            SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();
            string username = myCharacterBio.Username;
            string selectQuery = "SELECT * FROM dbo.CharacterDesign WHERE username = '" + username + "'";
            SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

            SqlDataReader reader = selectCommand.ExecuteReader();

            while (reader.Read())
            {
                string DBskin_color = reader["skin_color"].ToString();
                string DBhair_style= reader["hair_style"].ToString();
                string DBhair_color = reader["hair_color"].ToString();
                string DBbody_type = reader["body_type"].ToString();
                string DBshirt_color = reader["shirt_color"].ToString();
                string DBpants_color = reader["pants_color"].ToString();
                string DBshoe_color = reader["shoe_color"].ToString();
                string DBaccessory = reader["accessory"].ToString();

                //Display the data inside the DB
                Console.WriteLine("\tSkin color:\t" + DBskin_color);
                Console.WriteLine("\tHair style:\t" + DBhair_style);
                Console.WriteLine("\tHair color:\t" + DBhair_color);
                Console.WriteLine("\tBody type:\t" + DBbody_type);
                Console.WriteLine("\tShirt color:\t" + DBshirt_color);
                Console.WriteLine("\tPants color:\t" + DBpants_color);
                Console.WriteLine("\tShoe color:\t" + DBshoe_color);
                Console.WriteLine("\tAccessory:\t" + DBaccessory);
                Console.WriteLine();
            }

            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
    public string HairStyle
    {
        get { return hair_style; }
        set { this.hair_style = value; }
    }
    public string HairColor
    {
        get { return hair_color; }
        set { this.hair_color = value; }
    }
    public string SkinColor
    {
        get { return skin_color; }
        set { this.skin_color = value; }
    }
    public string BodyType
    {
        get { return body_type; }
        set { this.body_type = value; }
    }
    public string ShirtColor
    {
        get { return shirt_color; }
        set { this.shirt_color = value; }
    }
    public string PantsColor
    {
        get { return pants_color; }
        set { this.pants_color = value; }
    }
    public string ShoeColor
    {
        get { return shoe_color; }
        set { this.shoe_color = value; }
    }
    public string Accessory
    {
        get { return accessory; }
        set { this.accessory = value; }
    }
}

//INHERITANCE
public class CharacterType : ICharacterType
{
    private string character_class, character_element, body_armor, leg_armor, boots;

    //CONSTRUCTOR
    public CharacterType()
    {
        Console.WriteLine("\n-- CHARACTER TYPE --");
    }

    public void DisplayCharacterType(string SQLConnectionString, CharacterBiography myCharacterBio)
    {
        try
        {
            SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            string username = myCharacterBio.Username;
            string selectQuery = "SELECT * FROM dbo.CharacterType WHERE username = '" + username + "'";
            SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

            SqlDataReader reader = selectCommand.ExecuteReader();

            while (reader.Read())
            {
                string DBcharacter_class = reader["character_class"].ToString();
                string DBcharacter_element = reader["character_element"].ToString();
                string DBbody_armor = reader["body_armor"].ToString();
                string DBleg_armor = reader["leg_armor"].ToString();
                string DBboots = reader["boots"].ToString();

                //dispplays the data inside the DB
                Console.WriteLine("\tCharacter class:\t" + DBcharacter_class);
                Console.WriteLine("\tCharacter element:\t" + DBcharacter_element);
                Console.WriteLine("\tBody Armor:\t\t" + DBbody_armor);
                Console.WriteLine("\tLeg Armor:\t\t" + DBleg_armor);
                Console.WriteLine("\tboots:\t\t\t" + DBboots);
                Console.WriteLine();
            }

            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
    public string CharacterClass
    {
        get { return character_class; }
        set { this.character_class = value; }
    }
    public string CharacterElement
    {
        get { return character_element; }
        set { this.character_element = value; }
    }
    public string BodyArmor
    {
        get { return body_armor; }
        set { this.body_armor = value; }
    }
    public string LegArmor
    {
        get { return leg_armor; }
        set { this.leg_armor = value; }
    }
    public string Boots
    {
        get { return boots; }
        set { this.boots = value; }
    }
}

//INHERITANCE
public class CharacterStats : ICharacterStats
{
    private int strength, dexterity, intelligence;
    
    //CONSTRUCTOR
    public CharacterStats()
    {
        Console.WriteLine("\n-- CHARACTER STATS --");
    }

    public void DisplayCharacterStats(string SQLConnectionString, CharacterBiography myCharacterBio)
    {
        try
        {
            SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            string username = myCharacterBio.Username;
            string selectQuery = "SELECT * FROM dbo.CharacterStats WHERE username = '" + username + "'";
            SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

            SqlDataReader reader = selectCommand.ExecuteReader();

            while (reader.Read())
            {
                string DBstrength = reader["strength"].ToString();
                string DBdexterity = reader["dexterity"].ToString();
                string DBintelligence = reader["intelligence"].ToString();

                //Displays the data inside the DB
                Console.WriteLine("\tStrength:\t" + DBstrength);
                Console.WriteLine("\tDexterity:\t" + DBdexterity);
                Console.WriteLine("\tintelligence:\t" + DBintelligence);
                Console.WriteLine();
            }

            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }

    }
    public int Strength
    {
        get { return strength; }
        set { this.strength = value; }
    }
    public int Dexterity
    {
        get { return dexterity; }
        set { this.dexterity = value; }
    }
    public int Intelligence
    {
        get { return intelligence; }
        set { this.intelligence = value; }
    }
}

//INHERITANCE
public class CharacterCompanion : ICharacterCompanion
{
    private string companion, companion_element;

    //CONSTRUCTOR
    public CharacterCompanion()
    {
        Console.WriteLine("\n-- CHARACTER COMPANION --");
    }

    public void DisplayCharacterCompanion(string SQLConnectionString, CharacterBiography myCharacterBio)
    {
        try
        {
            SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            string username = myCharacterBio.Username;
            string selectQuery = "SELECT * FROM dbo.CharacterCompanion WHERE username = '" + username + "'";
            SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

            SqlDataReader reader = selectCommand.ExecuteReader();

            while (reader.Read())
            {
                string DBcompanion = reader["companion"].ToString();
                string DBcompanion_element = reader["companion_element"].ToString();

                //Displays the data inside the DB
                Console.WriteLine("\tCompanion:\t\t" + DBcompanion);
                Console.WriteLine("\tCompanion Element:\t" + DBcompanion_element);
                Console.WriteLine();
            }

            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }/*
        Console.WriteLine("\tCompanion:\t\t" + companion);
        Console.WriteLine("\tCompanion Element:\t" + companion_element);*/
    }
    
    public string Companion
    {
        get { return companion; }
        set { this.companion = value; }
    }
    public string CompanionElement
    {
        get { return companion_element; }
        set { this.companion_element = value; }
    }
}

//INHERITANCE
public class IsNewPlayer : IIsNewPlayer
{
    private bool isNew;

    public bool IsNew
    {
        get { return isNew; }
        set { this.isNew = value; }
    }

    public void DisplayPlayerExperience()
    {
        if (isNew == true)
        {
            Console.WriteLine("The Player is new to the game.");
        } else if (isNew == false)
        {
            Console.WriteLine("The Player is experienced in the game.");
        }
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        SqlConnection SQLConnect;
        string SQLConnectionString = @"Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=C:\USERS\ADRIAN\SOURCE\REPOS\CHARACTERCREATIONPROGRAM\CHARACTERCREATIONPROGRAM\DATABASE1.MDF;Integrated Security=True";

        // DB connection
        // method to delete all character in the DB
        /*try
        {
            SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            //string insertQuery = "INSERT INTO dbo.Character (DBusername, DBnickname, DBgender, DBpronouns, DBbio) VALUES('hatdog', 'AYAN', 'male', 'he', 'Nothing...')";
            string insertQuery = "DELETE FROM dbo.Character\nDELETE FROM dbo.CharacterDesign\nDELETE FROM dbo.CharacterType\nDELETE FROM dbo.CharacterStats\nDELETE FROM dbo.CharacterCompanion\nDELETE FROM dbo.CharacterExperience";
            SqlCommand Insert = new SqlCommand(insertQuery, SQLConnect);

            // Execute the query
            Insert.ExecuteNonQuery();

            // Close the connection
            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }*/

        Console.WriteLine("Welcome to Character Creation Program!\n");

        //MENU METHOD
        CharacterMenu(SQLConnectionString);

        //CHARACTER BIOGRAPHY
        CharacterBiography myCharacterBio = new CharacterBiography();

        //Name
        InputUsername(myCharacterBio, SQLConnectionString);
        InputNickname(myCharacterBio);

        //Gender Identity
        InputGender(myCharacterBio);
        InputPronouns(myCharacterBio);
        InputBio(myCharacterBio);

        Console.WriteLine();
        // myCharacterBio.DisplayCharacterBiography(SQLConnectionString, myCharacterBio);

        //CHARACTER DESIGN
        CharacterDesign myCharacterDesign = new CharacterDesign();

        PickSkinColor(myCharacterDesign);
        //Head
        PickHairStyle(myCharacterDesign);
        PickHairColor(myCharacterDesign);

        //Body
        PickBodyType(myCharacterDesign);
        PickShirtColor(myCharacterDesign);
        PickPantsColor(myCharacterDesign);
        PickShoeColor(myCharacterDesign);

        //Accessory
        PickAccessory(myCharacterDesign);
        
        Console.WriteLine();
        // myCharacterDesign.DisplayCharacterDesign(SQLConnectionString, myCharacterBio);

        //CHARACTER TYPE
        CharacterType myCharacterType = new CharacterType();

        //Character Class
        PickCharacterClass(myCharacterType);
        PickCharacterElement(myCharacterType);

        //Armors
        PickBodyArmor(myCharacterType);
        PickLegArmor(myCharacterType);
        PickBoots(myCharacterType);

        Console.WriteLine();
        myCharacterType.DisplayCharacterType(SQLConnectionString, myCharacterBio);

        //CHARACTER STATS
        CharacterStats myCharacterStats = new CharacterStats();
        UpgradeCharacterStats(myCharacterStats);

        
        Console.WriteLine();
        // myCharacterStats.DisplayCharacterStats(SQLConnectionString, myCharacterBio);

        //CHARACTER COMPANION
        CharacterCompanion myCharacterCompanion = new CharacterCompanion();

        //Companion
        ChooseCompanion(myCharacterCompanion);
        ChooseCompanionElement(myCharacterCompanion);

        // save bio to DB
        //DBusername, DBnickname, DBgender, DBpronouns, DBbio
        try
        {
            SqlConnection SQLConnection = new SqlConnection(SQLConnectionString);
            SQLConnection.Open();

            // Save bio to DB
            string InsertBioQueryString = "INSERT INTO dbo.Character (username, nickname, gender, pronouns, bio) VALUES('" +
                myCharacterBio.Username + "', '" + myCharacterBio.Nickname + "', '" +
                myCharacterBio.Gender + "', '" + myCharacterBio.Pronouns + "', '" + myCharacterBio.Bio + "')";

            SqlCommand InsertBio = new SqlCommand(InsertBioQueryString, SQLConnection);
            InsertBio.ExecuteNonQuery();

            // Save design to DB
            string InsertDesignQueryString = "INSERT INTO dbo.CharacterDesign (username, skin_color, hair_style, hair_color, body_type, shirt_color, pants_color, shoe_color, accessory) " +
                "VALUES('" + myCharacterBio.Username + "', '" + myCharacterDesign.SkinColor + "', '" +
                myCharacterDesign.HairStyle + "', '" + myCharacterDesign.HairColor + "', '" +
                myCharacterDesign.BodyType + "', '" + myCharacterDesign.ShirtColor + "', '" +
                myCharacterDesign.PantsColor + "', '" + myCharacterDesign.ShoeColor + "', '" + myCharacterDesign.Accessory + "')";

            SqlCommand InsertDesign = new SqlCommand(InsertDesignQueryString, SQLConnection);
            InsertDesign.ExecuteNonQuery();

            // Save type to DB
            string InsertTypeQueryString = "INSERT INTO dbo.CharacterType (username, character_class, character_element, body_armor, leg_armor, boots) " +
                "VALUES('" + myCharacterBio.Username + "', '" + myCharacterType.CharacterClass + "', '" +
                myCharacterType.CharacterElement + "', '" + myCharacterType.BodyArmor + "', '" +
                myCharacterType.LegArmor + "', '" + myCharacterType.Boots + "')";

            SqlCommand InsertType = new SqlCommand(InsertTypeQueryString, SQLConnection);
            InsertType.ExecuteNonQuery();

            // Save stats to DB
            string InsertStatsQueryString = "INSERT INTO dbo.CharacterStats (username, strength, dexterity, intelligence) " +
                "VALUES('" + myCharacterBio.Username + "', '" + myCharacterStats.Strength + "', '" +
                myCharacterStats.Dexterity + "', '" + myCharacterStats.Intelligence + "')";

            SqlCommand InsertStats = new SqlCommand(InsertStatsQueryString, SQLConnection);
            InsertStats.ExecuteNonQuery();

            // Save companion to DB
            string InsertCompanionQueryString = "INSERT INTO dbo.CharacterCompanion (username, companion, companion_element) " +
                "VALUES('" + myCharacterBio.Username + "', '" + myCharacterCompanion.Companion + "', '" +
                myCharacterCompanion.CompanionElement + "')";

            SqlCommand InsertCompanion = new SqlCommand(InsertCompanionQueryString, SQLConnection);
            InsertCompanion.ExecuteNonQuery();

            SQLConnection.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }

        Console.WriteLine();
        // myCharacterCompanion.DisplayCharacterCompanion(SQLConnectionString, myCharacterBio);

        try
        {
            while (true)
            {
                SQLConnect = new SqlConnection(SQLConnectionString);
                SQLConnect.Open();

                Console.WriteLine("\n\t[1] Display Character\n\t[2] Delete Character");
                string choice = Console.ReadLine();

                if (choice.Equals("1"))
                {
                    //display all stats
                    myCharacterBio.DisplayCharacterBiography(SQLConnectionString, myCharacterBio);
                    myCharacterDesign.DisplayCharacterDesign(SQLConnectionString, myCharacterBio);
                    myCharacterType.DisplayCharacterType(SQLConnectionString, myCharacterBio);
                    myCharacterStats.DisplayCharacterStats(SQLConnectionString, myCharacterBio);
                    myCharacterCompanion.DisplayCharacterCompanion(SQLConnectionString, myCharacterBio);
                    break;
                }
                else if (choice.Equals("2"))
                {
                    //delete character
                    string DeleteCharacterQuery = "DELETE FROM dbo.Character WHERE username = '" + myCharacterBio.Username + "'\n" +
                        "DELETE FROM dbo.CharacterDesign WHERE username = '" + myCharacterBio.Username + "'\n" +
                        "DELETE FROM dbo.CharacterType WHERE username = '" + myCharacterBio.Username + "'\n" +
                        "DELETE FROM dbo.CharacterStats WHERE username = '" + myCharacterBio.Username + "'\n" +
                        "DELETE FROM dbo.CharacterCompanion WHERE username = '" + myCharacterBio.Username + "'\n" +
                        "DELETE FROM dbo.CharacterExperience WHERE username = '" + myCharacterBio.Username + "'\n";

                    SqlCommand Delete = new SqlCommand(DeleteCharacterQuery, SQLConnect);
                    Delete.ExecuteNonQuery();
                    SQLConnect.Close();

                    Console.WriteLine("Character Deleted. Exiting program...");
                    Environment.Exit(0);
                    break;
                }
                else
                {
                    Console.WriteLine("Oop! Wrong input. Please try again.");
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }

        //USER'S GAME EXPERIENCE
        IsNewPlayer isPlayerNew = new IsNewPlayer();
        Console.WriteLine();
        CheckIfNewPlayer(isPlayerNew);
        CheckIfNewPlayer(isPlayerNew, isPlayerNew.IsNew, myCharacterBio);

        //
        try
        {
            SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            int checkIfNew;
            if (isPlayerNew.IsNew)
            {
                checkIfNew = 1;
            }
            else
            {
                checkIfNew = 0;
            }

            string InsertExperienceQueryString = "INSERT INTO dbo.CharacterExperience (username, isNew) VALUES('" +
                myCharacterBio.Username + "', " +
                checkIfNew + ")";
            SqlCommand Insert = new SqlCommand(InsertExperienceQueryString, SQLConnect);
            Insert.ExecuteNonQuery();
            SQLConnect.Close();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }


    }

    private static void CharacterMenu(string SQLConnectionString)
    {
        Console.WriteLine("Enter Action:\n\t[1] Create a Character\n\t[2] Delete a character\n\t[3] Display all character(s)\n\t[4] Exit program");
        string decide = Console.ReadLine();

        if (decide.Equals("1"))
        {
            Console.WriteLine("Proceeding to Character Creation...\n");
        }
        else if (decide.Equals("2"))
        {
            Console.WriteLine("Enter username that you want to delete: ");
            String DeleteCharacter = Console.ReadLine();

            while (true) {
                if (!String.IsNullOrWhiteSpace(DeleteCharacter))
                {
                    break;
                }
                else
                {
                    Console.WriteLine("Oops! Invaalid input. Please enter a character.");
                    CharacterMenu(SQLConnectionString);
                    break;
                }
            }

            // check if the username is in the DB exist
            SqlConnection SQLConnect;
            SQLConnect = new SqlConnection(SQLConnectionString);
            SQLConnect.Open();

            string CheckUsernameIfExistQuery = "SELECT * FROM dbo.Character WHERE username = '" + DeleteCharacter + "'";

            SqlCommand CheckUsername = new SqlCommand(CheckUsernameIfExistQuery, SQLConnect);

            SqlDataReader reader = CheckUsername.ExecuteReader();
            string usernameInDB = "";

            while (reader.Read())
            {
                usernameInDB = reader["username"].ToString();

                if (usernameInDB.Equals(DeleteCharacter))
                {
                    Console.WriteLine("Character found... Deleting Character...");
                    if (!String.IsNullOrEmpty(DeleteCharacter))
                    {
                        //enter method here to delete a character
                        try
                        {
                            string DeleteCharacterQuery = "DELETE FROM dbo.Character WHERE username = '" + DeleteCharacter + "'";
                            SqlConnection SqlConnect;
                            SqlConnect = new SqlConnection(SQLConnectionString);
                            SqlConnect.Open();

                            SqlCommand Delete = new SqlCommand(DeleteCharacterQuery, SqlConnect);
                            Delete.ExecuteNonQuery();

                            Console.WriteLine("Character Successfully Deleted.\n");
                        } catch(Exception ex)
                        {
                            Console.WriteLine("Error:" +  ex.Message);
                        }
                        Main(null);
                    }
                    else if (String.IsNullOrEmpty(DeleteCharacter))
                    {
                        Console.WriteLine("Oops! Invaid input. Username cannot be blank.");
                        CharacterMenu(SQLConnectionString);
                    }
                    else
                    {
                        Console.WriteLine("Oops! Invalid input. Please try again.");
                    }
                    break;
                }
            }

            if (!usernameInDB.Equals(DeleteCharacter)){
                Console.WriteLine("Oops! Character not found. Please try again.");
                CharacterMenu(SQLConnectionString);
            }
            SQLConnect.Close();
            //

            
        }
        else if (decide.Equals("3")) // Display all characters in the DB
        {
            try
            {
                SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
                SQLConnect.Open();

                string selectQuery = "SELECT * FROM dbo.Character";
                SqlCommand selectCommand = new SqlCommand(selectQuery, SQLConnect);

                SqlDataReader reader = selectCommand.ExecuteReader();

                bool checkICharacterExist = false;
                while (reader.Read())
                {
                    string DBusername = reader["username"].ToString();
                    
                    /*if (string.IsNullOrEmpty(DBusername))
                    {
                        Console.WriteLine("There is no Characters created at the moment...");
                    }*/

                    /*string DBnickname = reader["nickname"].ToString();
                    string DBgender = reader["gender"].ToString();
                    string DBpronouns = reader["pronouns"].ToString();
                    string DBbio = reader["bio"].ToString();*/

                    //Display the data inside the DB
                    Console.WriteLine("\tUsername:\t" + DBusername);
                    /*Console.WriteLine("\tNickname:\t" + DBnickname);
                    Console.WriteLine("\tGender:\t\t" + DBgender);
                    Console.WriteLine("\tPronouns:\t" + DBpronouns);
                    Console.WriteLine("\tBio:\t\t" + DBbio);*/
                    Console.WriteLine();

                    checkICharacterExist = true;
                    
                }
                if (!checkICharacterExist)
                {
                    Console.WriteLine("There is no Characters created at the moment...");
                }

                SQLConnect.Close();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
            CharacterMenu(SQLConnectionString);
        }
        else if (decide.Equals("4"))
        {
            Console.WriteLine("Exiting program...");
            Environment.Exit(0);
        }
        else
        {
            Console.WriteLine("Oops! Invalid action. Please enter a valid key.");
            CharacterMenu(SQLConnectionString) ;
        }
    }

    //STRUCTURE
    struct CharacterOptions
    {
        //Compation
        public string[] companion_element;
        public string[] companions;
        
        //Character Stats
        public string[] stats;
        
        //Character Type
        public string[] boots;
        public string[] leg_armor;
        public string[] body_armor;
        public string[] character_element;
        public string[] character_class;
        
        //Character Design
        public string[] accessories;
        public string[] shoe_colors;
        public string[] pants_colors;
        public string[] shirt_colors;
        public string[] skin_colors;
        public string[] body_types;
        public string[] hair_colors;
        public string[] hair_styles;
    }

    //METHOD OVERRIDING
    private static void CheckIfNewPlayer(IsNewPlayer isPlayerNew, Boolean isNew, CharacterBiography myCharacterBio)
    {
        if (isNew)
        {
            Console.WriteLine("Our fierce some adventurer " + myCharacterBio.Nickname + " is about to go on adventure to defeat the demon lord, but before going in a venture you must train to be well prepared!");
            Environment.Exit(0);
        }
        else if (!isNew)
        {
            Console.WriteLine("Our fierce some adventurer " + myCharacterBio.Nickname + " is about to go on adventure to defeat the demon lord, it seems that he is well prepared! Good luck on your journey adventurer.");
            Environment.Exit(0);
        }
    }
    private static void CheckIfNewPlayer(IsNewPlayer isPlayerNew)
    {
        try
        {
            Console.WriteLine("Are you a new player?\n\t[1] Yes\n\t[2] No");

            if (int.TryParse(Console.ReadLine(), out int choice) && choice.Equals(1))
            {
                isPlayerNew.IsNew = true;
            }
            else if (choice.Equals(2))
            {
                isPlayerNew.IsNew = false;
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                CheckIfNewPlayer(isPlayerNew);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Oops! Invalid input. " + ex.Message);
            CheckIfNewPlayer(isPlayerNew);
        }
    }

    private static void ChooseCompanionElement(CharacterCompanion myCharacterCompanion)
    {
        try
        {
            CharacterOptions options;
            options.companion_element = new string[]{ "Earth", "Water", "Fire", "Wind" };
            Console.WriteLine("Choose your companion element:");
            for (int i = 0; i < options.companion_element.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.companion_element[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenCompanionElement) && chosenCompanionElement >= 1 && chosenCompanionElement <= options.companion_element.Length)
            {
                myCharacterCompanion.CompanionElement = options.companion_element[chosenCompanionElement - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                ChooseCompanionElement(myCharacterCompanion);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
            ChooseCompanionElement(myCharacterCompanion);
        }
    }

    private static void ChooseCompanion(CharacterCompanion myCharacterCompanion)
    {
        try
        {
            CharacterOptions options;
            options.companions = new string[] { "Wolf", "Cat", "Dog", "Bird" };
            Console.WriteLine("Choose your companion:");
            for (int i = 0; i < options.companions.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.companions[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenCompanion) && chosenCompanion >= 1 && chosenCompanion <= options.companions.Length)
            {
                myCharacterCompanion.Companion = options.companions[chosenCompanion - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                ChooseCompanion(myCharacterCompanion);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Oops! Invalid input. " + ex.Message);
            ChooseCompanion(myCharacterCompanion);
        }
    }

    private static void UpgradeCharacterStats(CharacterStats myCharacterStats)
    {
        try
        {
            CharacterOptions options;
            Console.WriteLine("You have 4 free upgrades int the folllowing.");

            options.stats = new string[] { "Strength", "Dexterity", "Intelligence" };
            foreach (string stat in options.stats)
            {
                Console.WriteLine("\t- " + stat);
            }

            Console.WriteLine("Enter upgrades for the following:");

            int maxUpgrade = 4;
            int Strength = 0;
            int Dexterity = 0;
            int Intelligence = 0;

            foreach (string stat in options.stats)
            {
                while (maxUpgrade > 0)
                {
                    Console.Write("\nRemaining upgrades: " + maxUpgrade + "\n" + stat + ":\t");
                    
                    if (int.TryParse(Console.ReadLine(), out int inputUpgrade) && inputUpgrade >= 0 && inputUpgrade <= maxUpgrade)
                    {
                        maxUpgrade -= inputUpgrade;

                        switch (stat)
                        {
                            case "Strength":
                                Strength = inputUpgrade;
                                myCharacterStats.Strength = Strength;
                                break;
                            case "Dexterity":
                                Dexterity = inputUpgrade;
                                myCharacterStats.Dexterity = Dexterity;
                                break;
                            case "Intelligence":
                                Intelligence = inputUpgrade;
                                myCharacterStats.Intelligence = Intelligence;
                                break;
                        }
                        break;
                    }
                    Console.WriteLine("Invalid input. Please try agan later.");
                }
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            UpgradeCharacterStats(myCharacterStats);
        }
    }

    private static void PickBoots(CharacterType myCharacterType)
    {
        try
        {
            CharacterOptions options;
            options.boots = new string[] { "Leather boots", "Leather sandals", "Scrap boots" };
            Console.WriteLine("Choose your boots:");
            for (int i = 0; i < options.boots.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.boots[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenBoots) && chosenBoots >= 1 && chosenBoots <= options.boots.Length)
            {
                myCharacterType.Boots = options.boots[chosenBoots - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickBoots(myCharacterType);
            }
        }catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickBoots(myCharacterType);
        }
    }

    private static void PickLegArmor(CharacterType myCharacterType)
    {
        try
        {
            CharacterOptions options;
            options.leg_armor = new string[] { "Leather pants", "Cotton shorts", "Silk skirts" };
            Console.WriteLine("Choose your leg armor:");
            for (int i = 0; i < options.leg_armor.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.leg_armor[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenLegArmor) && chosenLegArmor >= 1 && chosenLegArmor <= options.leg_armor.Length)
            {
                myCharacterType.LegArmor = options.leg_armor[chosenLegArmor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickLegArmor(myCharacterType);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickLegArmor(myCharacterType);
        }
    }

    private static void PickBodyArmor(CharacterType myCharacterType)
    {
        try
        {
            CharacterOptions options;
            options.body_armor = new string[] { "Leather armor", "Leather robe", "Cotton tunic" };
            Console.WriteLine("Choose your body armor:");
            for (int i = 0; i < options.body_armor.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.body_armor[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenBodyArmor) && chosenBodyArmor >= 1 && chosenBodyArmor <= options.body_armor.Length)
            {
                myCharacterType.BodyArmor = options.body_armor[chosenBodyArmor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickBodyArmor(myCharacterType);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickBodyArmor(myCharacterType);
        }
    }

    private static void PickCharacterElement(CharacterType myCharacterType)
    {
        try
        {
            CharacterOptions options;
            options.character_element = new string[] { "Earth", "Water", "Fire", "Wind" };
            Console.WriteLine("Choose your element:");
            for (int i = 0; i < options.character_element.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.character_element[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenCharacterElement) && chosenCharacterElement >= 1 && chosenCharacterElement <= options.character_element.Length)
            {
                myCharacterType.CharacterElement = options.character_element[chosenCharacterElement - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickCharacterElement(myCharacterType);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickCharacterElement(myCharacterType);
        }
    }

    private static void PickCharacterClass(CharacterType myCharacterType)
    {
        try
        {
            CharacterOptions options;
            options.character_class = new string[] { "Swordsman", "Rouge", "Assasin", "Cleric", "Paladin", "Wizard", "Alchemist" };
            Console.WriteLine("Choose your class:");
            for (int i = 0; i < options.character_class.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.character_class[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenCharacterClass) && chosenCharacterClass >= 1 && chosenCharacterClass <= options.character_class.Length)
            {
                myCharacterType.CharacterClass = options.character_class[chosenCharacterClass - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickCharacterClass(myCharacterType);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickCharacterClass(myCharacterType);
        }
    }

    private static void PickAccessory(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.accessories = new string[] { "Health gem", "Griomoir book", "Divine Shield", "Mana gem", "Wind archer lace", "Gauntlet", "Magic Cloak", "Shadowstep Boots" };
            Console.WriteLine("Choose accessory");
            for (int i = 0; i < options.accessories.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.accessories[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenAccessory) && chosenAccessory >= 1 && chosenAccessory <= options.accessories.Length)
            {
                myCharacterDesign.Accessory = options.accessories[chosenAccessory - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickAccessory(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickAccessory(myCharacterDesign);
        }
    }

    private static void PickShoeColor(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.shoe_colors = new string[] { "White", "Black", "Red", "Blue", "Green", "Yellow", "Purple", "Orange", "Gray", "Pink" };
            Console.WriteLine("Choose shoe color:");
            for (int i = 0; i < options.shoe_colors.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.shoe_colors[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenShoeColor) && chosenShoeColor >= 1 && chosenShoeColor <= options.shoe_colors.Length)
            {
                myCharacterDesign.ShoeColor = options.shoe_colors[chosenShoeColor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickShoeColor(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickShoeColor(myCharacterDesign);
        }
    }

    private static void PickPantsColor(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.pants_colors = new string[] { "White", "Black", "Red", "Blue", "Green", "Yellow", "Purple", "Orange", "Gray", "Pink" };
            Console.WriteLine("Choose pants color:");
            for (int i = 0; i < options.pants_colors.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.pants_colors[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenPantsColor) && chosenPantsColor >= 1 && chosenPantsColor <= options.pants_colors.Length)
            {
                myCharacterDesign.PantsColor = options.pants_colors[chosenPantsColor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickPantsColor(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickPantsColor(myCharacterDesign);
        }
    }

    private static void PickShirtColor(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.shirt_colors = new string[] { "White", "Black", "Red", "Blue", "Green", "Yellow", "Purple", "Orange", "Gray", "Pink" };
            Console.WriteLine("Choose shirt color:");

            for (int i = 0; i < options.shirt_colors.Length; i++) 
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.shirt_colors[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenShirtColor) && chosenShirtColor > 0 && chosenShirtColor <= options.shirt_colors.Length)
            {
                myCharacterDesign.ShirtColor = options.shirt_colors[chosenShirtColor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickShirtColor(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickShirtColor(myCharacterDesign);
        }
    }

    private static void PickBodyType(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.body_types = new string[] { "Slim", "Athletic", "Curvy", "Muscular", "Petite", "Hourglass", "Stocky", "Full-Figured", "Tall and Lean", "Pear-Shaped" };
            Console.WriteLine("Choose body type:");
            for (int i = 0; i < options.body_types.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.body_types[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenBodyType) && chosenBodyType >= 1 && chosenBodyType <= options.body_types.Length)
            {
                myCharacterDesign.BodyType = options.body_types[chosenBodyType - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickBodyType(myCharacterDesign);
            }
        }catch(FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickBodyType(myCharacterDesign);
        }
    }

    private static void PickHairColor(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.hair_colors = new string[] { "Jet Black", "Dark Brown", "Light Brown", "Auburn", "Red", "Blonde", "Strawberry Blonde", "Ash Blonde", "Platinum Blonde", "Silver Gray" };
            Console.WriteLine("Choose hair color:");
            for (int i = 0; i < options.hair_colors.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.hair_colors[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenHairColor) && chosenHairColor >= 1 && chosenHairColor <= options.hair_colors.Length)
            {
                myCharacterDesign.HairColor = options.hair_colors[chosenHairColor - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickHairColor(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickHairColor(myCharacterDesign);
        }
    }

    private static void PickHairStyle(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.hair_styles = new string[] { "Warrior Braid", "Skinny Head", "Top Knot Trek", "Glyphs Mohawk", "Starry Slickback", "Infusion ponytail" };
            Console.WriteLine("Choose hairstyle:");
            for (int i = 0; i < options.hair_styles.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.hair_styles[i]);
            }
            
            if (int.TryParse(Console.ReadLine(), out int chosenHairStyle) && chosenHairStyle >= 1 && chosenHairStyle <= options.hair_styles.Length)
            {
                myCharacterDesign.HairStyle = options.hair_styles[chosenHairStyle - 1];
            }
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickHairStyle(myCharacterDesign);
            }
        }
        catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickHairStyle(myCharacterDesign);
        }
    }

    private static void PickSkinColor(CharacterDesign myCharacterDesign)
    {
        try
        {
            CharacterOptions options;
            options.skin_colors = new string[] { "Pale Ivory", "Rich Ebony", "Olive tan", "Warm Caramel", "Deep Mahogany", "Rosy Beige" };
            Console.WriteLine("Choose skin color:");
            for (int i = 0; i < options.skin_colors.Length; i++)
            {
                Console.WriteLine("\t[" + (i + 1) + "] " + options.skin_colors[i]);
            }

            if (int.TryParse(Console.ReadLine(), out int chosenSkinColor) && chosenSkinColor >=1 && chosenSkinColor <= options.skin_colors.Length)
            {
                myCharacterDesign.SkinColor = options.skin_colors[chosenSkinColor - 1];
            } 
            else
            {
                Console.WriteLine("Oops! Invalid input. Please enter a valid number.");
                PickSkinColor(myCharacterDesign);
            }
        } catch (FormatException ex)
        {
            Console.WriteLine("Invalid input. " + ex.Message);
            PickSkinColor(myCharacterDesign);
        }
    }

    private static void InputBio(CharacterBiography myCharacterBio)
    {
        Console.WriteLine("Enter your bio:\t");
        string bio = Console.ReadLine();

        //data validation
        if (String.IsNullOrEmpty(bio))
        {
            Console.WriteLine("Oops! bio cannot be empty. Please try again.");
            InputBio(myCharacterBio);
        }
        else if (String.IsNullOrWhiteSpace(bio) || bio.All(char.IsWhiteSpace))
        {
            Console.WriteLine("Oops! username can't contain whitespaces. Please try again.");
            InputBio(myCharacterBio);
        }
        else
        {
            myCharacterBio.Bio = bio;
        }
    }

    private static void InputPronouns(CharacterBiography myCharacterBio)
    {
        Console.WriteLine("Enter your pronouns:\t(Maximum of 6 Characters)");
        string pronouns = Console.ReadLine();

        //data validation
        if (String.IsNullOrEmpty(pronouns))
        {
            Console.WriteLine("Oops! Pronouns cannot be empty. Please try again.");
            InputPronouns(myCharacterBio);
        }
        else if (pronouns.Length > 6)
        {
            Console.WriteLine("Oops! You exceed maximum character. Please try again.");
            InputPronouns(myCharacterBio);
        }
        else if (pronouns.Contains(" "))
        {
            Console.WriteLine("Oops! pronouns can't contain whitespaces. Please try again.");
            InputPronouns(myCharacterBio);
        }
        else
        {
            myCharacterBio.Pronouns = pronouns;
        }
    }

    private static void InputGender(CharacterBiography myCharacterBio)
    {
        Console.WriteLine("Enter your gender:\t(Male or Female)");
        string gender = Console.ReadLine();

        //data validation
        if (string.Equals(gender, "Male", StringComparison.OrdinalIgnoreCase) ||
            string.Equals(gender, "Female", StringComparison.OrdinalIgnoreCase))
        {
            myCharacterBio.Gender = gender;
        }
        else
        {
            Console.WriteLine("Oops! Invalid gender input. Please enter 'Male' or 'Female'.");
            InputGender(myCharacterBio);
        }
    }

    private static void InputNickname(CharacterBiography myCharacterBio)
    {
        Console.WriteLine("Enter your Nickname:\t(Maximum of 10 Characters).");
        string nickname = Console.ReadLine();

        //data validation
        if (String.IsNullOrEmpty(nickname))
        {
            Console.WriteLine("Oop! Nickname cannot be empty. Please try again.");
            InputNickname(myCharacterBio);
        }
        else if (nickname.Length > 10)
        {
            Console.WriteLine("Oops! Nickname cannot be more than 10 characters. Try Again.");
            InputNickname(myCharacterBio);
        }
        else if (nickname.Contains(" "))
        {
            Console.WriteLine("Oops! nickname can't contain whitespaces. Please try again.");
            InputNickname(myCharacterBio);
        }
        else
        {
            myCharacterBio.Nickname = nickname;
        }
    }

    private static void InputUsername(CharacterBiography myCharacterBio, string SQLConnectionString)
    {
        while (true)
        {
            Console.WriteLine("Enter your Username:\t(Maximum of 20 Characters)");
            string username = Console.ReadLine();

            // method to check username if exist
            if (CheckIfUsernameExist(myCharacterBio, SQLConnectionString, username))
            {
                Console.WriteLine("Oops! Username already taken. Please use a different username.");
            }
            else if (String.IsNullOrEmpty(username))
            {
                Console.WriteLine("Oops! Username cannot be Empty. Please try again.");
            }
            else if (username.Length > 20)
            {
                Console.WriteLine("Oops! Username cannot be more than 20 characters. Try Again.");
            }
            else if (username.Contains(" "))
            {
                Console.WriteLine("Oops! Username can't contain whitespaces. Please try again.");
            }
            else
            {
                myCharacterBio.Username = username;
                break;
            }
        }
    }

    private static bool CheckIfUsernameExist(CharacterBiography myCharacterBio, string SQLConnectionString, string username)
    {
        SqlConnection SQLConnect = new SqlConnection(SQLConnectionString);
        SQLConnect.Open();

        string CheckUsernameIfExistQuery = "SELECT * FROM dbo.Character WHERE username = '" + username + "'";

        SqlCommand CheckUsername = new SqlCommand(CheckUsernameIfExistQuery, SQLConnect);

        SqlDataReader reader = CheckUsername.ExecuteReader();
        string usernameInDB;

        while (reader.Read())
        {
            usernameInDB = reader["username"].ToString();

            if (String.Compare(username, usernameInDB, StringComparison.OrdinalIgnoreCase) == 0)
            {
                return true;
            }
        }
        return false;
        SQLConnect.Close();
    }
}