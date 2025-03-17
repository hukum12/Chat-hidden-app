# Chat-hidden-app
All chats hide 
@Entity(tableName = "hidden_chats")
data class Chat(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val sender: String,
    val message: String,
    val timestamp: Long
)

@Dao
interface ChatDao {
    @Insert
    suspend fun insertChat(chat: Chat)

    @Query("SELECT * FROM hidden_chats ORDER BY timestamp DESC")
    fun getChats(): LiveData<List<Chat>>
}

@Database(entities = [Chat::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun chatDao(): ChatDao
}
