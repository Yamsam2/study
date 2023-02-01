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



## SQLite DB에서 가져오기 (cursor 사용)  

  
curcor에 테이블 넣기  
```java
sqlDB = resultDB.getReadableDatabase();  
Cursor cursor;  
cursor = sqlDB.rawQuery("SELECT * FROM log_library;", null);   
```
  
Curosr 이동방법  
  
 
cursor.moveToFirst() : Cursor를 제일 첫번째 행(Row)으로 이동 시킨다.  
cursor.moveToNext() : Cursor를 다음 행(Row)으로 이동 시킨다.  
cursor.moveToPrevious() : Cursor를 이전 행(Row)으로 이동 시킨다.  
cursor.moveToPosition(position) : Cursor를 해당 Position 행(Row)으로 이동 시킨다.  
cursor.moveToLast() : Cursor를 마지막 행(Row)으로 이동 시킨다.  


Cursor 변수에 담기  
원하는 row에 Cursor위치시키고,  
변수 = cursor.getString(index값)   



