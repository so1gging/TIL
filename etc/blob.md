# Blob
## Blob
- Binary Large Object
- 블랍 이라고 부른다.
- 멀티미디어 데이터를 다룰때 사용한다.
- 

### Blob 생성
```typescript
const newBlob = new Blob(array, options)
```

#### 매개변수 중 array는 여러 객체가 혼합된 Array를 보낼 수 있다.
```typescript
new Blob([new ArrayBuffer(data)], { type: 'video/mp4' });
new Blob(new Uint8Array(data), { type: 'image/png' });  
new Blob(['<div>Hello Blob!</div>'], {
  type: 'text/html',
  endings: 'native'
});
```

Blob URL

Blob 객체를 가리키는 URL 생성을 위해 `createObjectURL` 를 사용할 수 있다.

```typescript
URL.createObjectURL(blob)
// > blob:http://localhost:1234/28ff8746-94eb-4dbe-9d6c-2443b581dd30
```

아래처럼 활요앟ㄹ 수 있다.
```typescript
<img src="blob:http://localhost:1234/28ff8746-94eb-4dbe-9d6c-2443b581dd30" alt="Blob URL Image" />
```

**참고**
> https://heropy.blog/2019/02/28/blob/