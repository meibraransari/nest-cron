# Nest-Cron

## Node requirement
```
node -v
```
    ### v18.15.0

## Install nest
```
sudo npm install -g @nestjs/cli
```
## Create App
```
nest new nest-cron-app
```

## Install Required package
```
cd nest-cron-app
npm install --save @nestjs/schedule
nest generate service cron
```
## Modify file
```
// src/cron/cron.service.ts

import { Injectable, Logger } from '@nestjs/common';
import { Cron, CronExpression } from '@nestjs/schedule';

@Injectable()
export class CronService {
  private readonly logger = new Logger(CronService.name);

  @Cron(CronExpression.EVERY_MINUTE)
  handleCron() {
    const now = new Date();
    this.logger.debug(`Called at ${now.toISOString()}`);
  }
}
```
## Modify file
```
// src/app.module.ts

import { Module } from '@nestjs/common';
import { ScheduleModule } from '@nestjs/schedule';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { CronService } from './cron/cron.service';

@Module({
  imports: [ScheduleModule.forRoot()],
  controllers: [AppController],
  providers: [AppService, CronService],
})
export class AppModule {}
```

## Start App
```
npm run start
```

