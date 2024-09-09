private void AutoReplay(User user, Chat chat, ref string msgToReplay)
{
    if (chat.text.Length > 0)
    {
        var splitPesan = chat.text.Split(' ');
        var keyword = splitPesan[0];
        var param = string.Empty;

        if (splitPesan.Count() > 1) param = splitPesan[1];

        SaveUser(user);
        SaveChat(chat);
                
        var perintahBot = new PerintahBot();

        switch (keyword.ToLower())
        {
            case "/about":
                msgToReplay = string.Format(ABOUT, _currentVersion, AUTHOR, EMAIL, URL);
                break;1

            case "/bantuan":
                msgToReplay = string.Format(BANTUAN, _currentVersion, AUTHOR, EMAIL, URL);
                break;2

            case "/mulai":
                perintahBot.Mulai(user.user_id, ref msgToReplay);
                break;3

            case "/soal":
                perintahBot.Soal(user.user_id, ref msgToReplay);
                break;4

            case "/soalterakhir":
                perintahBot.SoalTerakhir(user.user_id, ref msgToReplay);
                break;5

            case "/jawab":
                perintahBot.Jawab(user.user_id, param, ref msgToReplay);                        
                break;6

            case "/batal":
                perintahBot.Batal(user.user_id, ref msgToReplay);
                break;7

            case "/selesai":
                perintahBot.Selesai(user.user_id, ref msgToReplay);                        
                break;8

            default:
                msgToReplay = string.Format(PERINTAH_SALAH, keyword.ToLower());
                break;9
        }

        Console.WriteLine("msgToReplay: {0}", msgToReplay);
    }
}
