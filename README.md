# Nest-Cron

This is intend to test nest cron job.

## Node requirement
```
node -v
```

v18.15.0


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

## Output
```
npm run start

> nest-cron-app@0.0.1 start
> nest start

[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [NestFactory] Starting Nest application...
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [InstanceLoader] AppModule dependencies initialized +27ms
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [InstanceLoader] DiscoveryModule dependencies initialized +0ms
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [InstanceLoader] ScheduleModule dependencies initialized +1ms
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [RoutesResolver] AppController {/}: +7ms
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [RouterExplorer] Mapped {/, GET} route +4ms
[Nest] 433815  - 15/07/2024, 12:47:15 pm     LOG [NestApplication] Nest application successfully started +16ms
[Nest] 433815  - 15/07/2024, 12:48:00 pm   DEBUG [CronService] Called at 2024-07-15T07:18:00.019Z
[Nest] 433815  - 15/07/2024, 12:49:00 pm   DEBUG [CronService] Called at 2024-07-15T07:19:00.018Z
[Nest] 433815  - 15/07/2024, 12:50:00 pm   DEBUG [CronService] Called at 2024-07-15T07:20:00.017Z
[Nest] 433815  - 15/07/2024, 12:51:00 pm   DEBUG [CronService] Called at 2024-07-15T07:21:00.017Z
[Nest] 433815  - 15/07/2024, 12:52:00 pm   DEBUG [CronService] Called at 2024-07-15T07:22:00.017Z
[Nest] 433815  - 15/07/2024, 12:53:00 pm   DEBUG [CronService] Called at 2024-07-15T07:23:00.017Z
[Nest] 433815  - 15/07/2024, 12:54:00 pm   DEBUG [CronService] Called at 2024-07-15T07:24:00.006Z
[Nest] 433815  - 15/07/2024, 12:55:00 pm   DEBUG [CronService] Called at 2024-07-15T07:25:00.019Z
[Nest] 433815  - 15/07/2024, 12:56:00 pm   DEBUG [CronService] Called at 2024-07-15T07:26:00.014Z
[Nest] 433815  - 15/07/2024, 12:57:00 pm   DEBUG [CronService] Called at 2024-07-15T07:27:00.017Z
[Nest] 433815  - 15/07/2024, 12:58:00 pm   DEBUG [CronService] Called at 2024-07-15T07:28:00.005Z
```

