# Xiaomi-Esp32-Oda-Termostat

Xamarin Android App UI


![WhatsApp Image 2023-01-03 at 14 41 20](https://user-images.githubusercontent.com/100942011/210350809-00200994-8cc0-44e1-a4e0-d0f618351cb1.jpeg)




FireBaseHelper Client 

        FirebaseClient firebase = new FirebaseClient("Your Client Address");
        
FireBaseHelper Operation

        public async Task<List<TermoModel>> GetTermoModels()
        {

            return (await firebase
              .Child("TermoModels")
              .OnceAsync<TermoModel>()).Select(item => new TermoModel
              {
                  Id = item.Object.Id,
                  hum = item.Object.hum,
                  bat = item.Object.bat,
                  temp = item.Object.temp
              }).ToList();
        }
        public async Task<List<AppModel>> GetAppModels()
        {

            return (await firebase
              .Child("AppModels")
              .OnceAsync<AppModel>()).Select(item => new AppModel
              {
                  Id = item.Object.Id,
                  sens = item.Object.sens,
                  temp = item.Object.temp,
                  status = item.Object.status
              }).ToList();
        }
        public async Task<AppModel> GetAppModel(int id)
        {
            var allPersons = await GetAppModels();
            await firebase
              .Child("AppModels")
              .OnceAsync<AppModel>();
            return allPersons.Where(a => a.Id == id).FirstOrDefault();
        }
        public async Task<TermoModel> GetTermoModel(int id)
        {
            var allPersons = await GetTermoModels();
            await firebase
              .Child("TermoModels")
              .OnceAsync<TermoModel>();
            return allPersons.Where(a => a.Id == id).FirstOrDefault();
        }
        public async Task AddAppModels(int id, int temp, int status, int sens)
        {
            await firebase
              .Child("AppModels")
              .PostAsync(new AppModel() { Id = id, temp = temp, status = status, sens = sens });
        }
        public async Task AddTermoModels(int id, int temp, int hum, int bat)
        {
            await firebase
              .Child("TermoModels")
              .PostAsync(new TermoModel() { Id = id, temp = temp, hum = hum, bat = bat });
        }
        public async Task UpdateAppModels(int id, int temp, int status, int sens)
        {
            var toUpdatePerson = (await firebase
              .Child("AppModels")
              .OnceAsync<AppModel>()).Where(a => a.Object.Id == id).FirstOrDefault();

            await firebase
              .Child("AppModels")
              .Child(toUpdatePerson.Key)
              .PutAsync(new AppModel() { Id = id, temp = temp, status = status, sens = sens });
        }
        
Arduino App

https://github.com/hlldgn/Xiaomi-Esp32-Oda-Termostat-

