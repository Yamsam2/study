# SQLite DB생성 페이지 예제   
  

    public class TestDB extends SQLiteOpenHelper {
        private Context context;
        private static final String DATABASE_NAME = "test.db";
        private static final int DATABASE_VERSION = 1;
        private static final String TABLE_NAME = "test_table";
        private static final String COLUMN_KEY = "_key";
        private static final String COLUMN_NAME = "name";
        private static final String COLUMN_AGE = "age";


        public TestDB(@Nullable Context context)
        {
            super(context, DATABASE_NAME, null, DATABASE_VERSION);
            this.context = context;
        }

        @Override
        public void onCreate(SQLiteDatabase db) {
            {
                String query = "CREATE TABLE " + TABLE_NAME
                        + " (" + COLUMN_KEY + " INTEGER PRIMARY KEY AUTOINCREMENT, "
                        + COLUMN_NAME + " TEXT, "
                        + COLUMN_AGE + " TEXT); ";
                db.execSQL(query);
            }
        }
        @Override
        public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

            db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);
            onCreate(db);
        }

        public void addBookTest(int key, String name, String age){
            SQLiteDatabase db = this.getWritableDatabase();
            ContentValues cv = new ContentValues();

            cv.put(COLUMN_KEY, key);
            cv.put(COLUMN_NAME, name);
            cv.put(COLUMN_AGE, age);

            long result = db.insert(TABLE_NAME, null, cv);

          if (result == -1)
          {
              Toast.makeText(context, "Failed Test", Toast.LENGTH_SHORT).show();
          }
          else
          {
              Toast.makeText(context, "succeed Test", Toast.LENGTH_SHORT).show();
          }

      }
      public void updateTest(int column1, String column2, String column3){
          SQLiteDatabase db = this.getWritableDatabase();
          String updateQuery = " UPDATE " + TABLE_NAME + " SET name ="+ "'"+column2+"'"+",age= "+"'"+column3+"'"+" WHERE _key="+"'"+column1+"'";
          db.execSQL(updateQuery);
          db.execSQL("SELECT * FROM test_table");
      }
  }
