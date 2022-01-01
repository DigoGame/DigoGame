- 👋 Hi, I’m @DigoGame
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
DigoGame/DigoGame is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
private IWhatsAppNETAPI _whatsAppApi; // deklarasi objek WhatsApp NET Clientprivate void btnStart_Click(object sender, EventArgs e){
    _whatsAppApi = new WhatsAppNETAPI​.​WhatsAppNETAPI​();

    var url = "https://web.whatsapp.com";

    using (new StCursor(Cursors.WaitCursor, new TimeSpan(0, 0, 0, 0)))
    {
        // buka chrome web browser untuk menjalankan WhatsApp Web
        if (_whatsAppApi.Connect(url))
        {
            while (!_whatsAppApi.OnReady())
            {
                Thread.Sleep(1000);
            }

            // subscribe event OnMessageRecieved 
            _whatsAppApi​.​OnMessageRecieved += OnMessageRecievedEventHandler​;
            _whatsAppApi​.​MessageSubscribe​();

            btnStart.Enabled = false;
            btnStop.Enabled = true;
        }
        else
            _whatsAppApi.Disconnect();
   private void OnMessageRecievedEventHandler​(​MsgArgs e){            
    var user = new User
    {
        user_id = e.Sender
    };

    var chat = new Chat
    {
        user_id = e.Sender,
        text = e.Msg
    };

    var msgToReplay = string.Empty;
    AutoReplay(user, chat, ref msgToReplay);

    _whatsAppApi.SendMessage(new MsgArgs(e.Sender, msgToReplay));} }}

