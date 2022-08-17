# Nestjs Static Serve With Flutter Web

## Pre Do

1. prepare build file
```bash
# create directory for flutter project
cd {flutter_dir}
# make new flutter project
flutter create .
# test web
flutter run -d chrome
# build web
flutter build web
# then you can see build files in build/web(COPY)
```

2. move nestjs directory and install nestjs serve static
```bash
npm i @nestjs/serve-static
```

3. set global prefix in main.ts file
```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.setGlobalPrefix('api');
  await app.listen(3000);
  console.log(`Application is running on: ${await app.getUrl()}`);
}
bootstrap();

```

4. set serve file path
```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ServeStaticModule } from '@nestjs/serve-static';
import { join } from 'path';

@Module({
  imports: [
    ServeStaticModule.forRoot({
      rootPath: join(__dirname, '..', 'web'),
      exclude: ['/api*'],
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

5. then paste build files in build/web before you copy in nestjs root path.

6. start the server
```bash
npm run start:dev
```



## Installation

```bash
$ npm install
```

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```
