# result

My Result Type Implementation for TypeScript.

## import

```ts
import { Result, ok, er } from '@charon1212/result';
```

## example

```ts
const returnResult = (flag: boolean): Result<string, { errorCode: number }> => {
  if (flag) return ok('success');
  else return er({ errorCode: 100 });
};
const returnVoidResult = (flag: boolean): Result<void, number> => {
  if (flag) return ok();
  else return er(100);
};
```

## interface

```ts
// * unwrap
ok('success').unwrap(); // 'success'
er('error').unwrap(); // throw 'error'

// * else
ok('success').else('some'); // 'success'
er('error').else('some'); // 'some'

// * handleOk
ok('success').handleOk(() => 'success2').unwrap(); // 'success2'
er('error').handleOk(() => 'success2').unwrap(); // throw 'error'

// * handleEr
ok('success').handleEr(() => 'error2').unwrap(); // 'success'
er('error').handleEr(() => 'error2').unwrap(); // throw 'error2'

// * match
ok('success').match({ ok: () => 'success3', er: () => 'error3' }); // 'success3'
er('error').match({ ok: () => 'success3', er: () => 'error3' }); // 'error3'

// * await
const promise: Promise<'promise'> = {} as any;
ok(promise).await(); // promise object of type Promise<Result<"promise", never>>
er(promise).await(); // promise object of type Promise<Result<never, "promise">>
```
