## State / Finite-State Machine
**Состояние** — это поведенческий паттерн проектирования, который позволяет объектам менять поведение в зависимости от своего состояния. Извне создаётся впечатление, что изменился класс объекта.
Отличие от Стратегии, в том, что и контекст, и конкретные состояния знают друг о друге и инициируют переход от одного состояния к другому.

Context
```ts
export class SideBar {
  public name = '';
  public value = this.state.sideBarState.normal;
  public icon = {
    left: this.state.sideBarIcon.hide,
    right: this.state.sideBarIcon.normal,
  };

  constructor(private state: State = new NormalState()) {
    this.transitionTo(state);
  }

  public transitionTo(state: State): void {
    this.state = state;
    this.state.setContext(this);
    this.name = this.state.constructor.name;
  }

  public onHideAction(): void {
    this.state.hide();
  }

  public onShowAction(): void {
    this.state.show();
  }
}
```
Abstract State class
```ts
export abstract class State {
  public sideBarState = {
    hide: '-382',
    normal: '0',
    extended: '980',
  };
  public sideBarIcon = {
    open: 'pi pi-angle-right',
    hide: 'pi pi-angle-left',
    normal: 'pi pi-angle-double-right',
    extended: 'pi pi-angle-double-left',
  };
  protected sidebar!: SideBar;

  public setContext(context: SideBar) {
    this.sidebar = context;
  }

  public hide(): void {
    this.sidebar.value = this.sideBarState.hide;
    this.sidebar.icon.right = this.sideBarIcon.open;
    this.sidebar.transitionTo(new HideState());
  };

  public abstract show(): void;
}
```
Concrete State class
```ts
export class HideState extends State {
  public show(): void {
    this.sidebar.value = this.sideBarState.normal;
    this.sidebar.icon.left = this.sideBarIcon.hide;
    this.sidebar.icon.right = this.sideBarIcon.normal;
    this.sidebar.transitionTo(new NormalState());
  }
}

export class NormalState extends State {
  public show(): void {
    this.sidebar.value = this.sideBarState.extended;
    this.sidebar.icon.left = this.sideBarIcon.hide;
    this.sidebar.icon.right = this.sideBarIcon.extended;
    this.sidebar.transitionTo(new ExtendedState());
  }
}

export class ExtendedState extends State {
  public show(): void {
    this.sidebar.value = this.sideBarState.normal;
    this.sidebar.icon.left = this.sideBarIcon.hide;
    this.sidebar.icon.right = this.sideBarIcon.normal;
    this.sidebar.transitionTo(new NormalState());
  }
}
```
Client code
```ts
import { SideBar } from './sidebar-state-machine';

@Component({
  ...
})
export class SomeComponent {
  public sidebar = new SideBar();
}
```
