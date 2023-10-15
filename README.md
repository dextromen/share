def get_daily(self):
        today = str(datetime.date.today())
        last_date = get_last_date()[0]
        daily_tryings = get_daily_tryings()
        
        todays_id = daily_tryings % 10 

        #check if todays day is the last date in db. if its today get last id. if not add todays date as last_date and 
        if last_date != today:
            add_last_date(today)
            update_daily_tryings(daily_tryings)
            ## get last 10 random daily ids
            randoms = get_everday_random()

             
            last_ten_readings = []
            for id in randoms:
                y = id['number']
                last_ten_readings.append(y)
                
            new_id = daily_tryings % 10            
            new_number = random.randint(1,78)
            while new_number  in last_ten_readings:
                new_number = random.randint(1,78)

            self.date_log[self.birthday] = new_number
            update_everyday_random(new_id,new_number)
            
                
            return new_number

        else:
            
            if len(self.first_birthday) == 0:
                x = int(get_todays_random(todays_id)[0][0])
                self.date_log[self.birthday] = x
                self.first_birthday.append(x)
                return x
            
            elif self.birthday in self.date_log:
                number = self.date_log[self.birthday]
                update_everyday_random(todays_id,number)
                return self.date_log[self.birthday]

            else:
                new = random.randint(1,78)
                self.date_log[self.birthday] = new
                update_everyday_random(todays_id,new)
            
                return new
