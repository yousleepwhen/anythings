### jest shallow 렌더링과 handler test 

mount 렌더를 shallow 렌더로 변경했을 때 발생한 몇가지 오류

before

```
...
const handler = jest.spyOn(wrapper.instance(), 'handler') 
const saveButton = wrapper.find('button')

saveButton.simulate('click')

expect(handler).toHaveBeenCalled() 
```

1. button 을 몾 찾음
 - Wrapped 된 StyledButton 컴포넌트 안 쪽에 button markup 이 존재할텐데 shallow 렌더링이라 못 찾음
 - StyledButton 의 displayName 을 'Button' 으로 변경하고 wrapper.find('Button') 으로 찾아 해결함

2. 하지만 mock 된 handler 가 호출되지 않았다고 나옴 
 - mount로 렌더링 했을 때는 모두 패스 됐었음
 - 구글링을 해봄
 - 렌더링 이전 시점에 컴포넌트 prototype 에 존재하는 핸들러를 spyOn 하라고 나와있음
 - 다른 방법으로는 wrapper의 instance 를 가져온 후 forceUpdate() 를 호출하거나 wrapper의 update() 를 호출
 - 근데 바로 위 방법은 나도 알고 있었다! 그런데 동작을 안했음
 - 하여간 spyOn 을 하는 시점이 mount든 shallow든 렌더링 되는 시점보다 더 빨라서 다른 곳에 바인딩 되서 나타나는 문제



after
```
const spy = jest.spyOn(TestComponent.prototype, 'handler')
const wrapper = shallow(<TestComponent />)

const saveButton = wrapper.find('Button')
saveButton.simulate('click')

expect(spy).toHaveBeenCalled()

```



