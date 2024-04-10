enum TypeControl { // Поле для ввода текста/ input = 0, // /Выпадающий список/ Select = 1 } 
 
abstract class Control { public abstract get options(): string[]; public abstract set options(val:string[]); 
 
protected abstract value: any; 
 
private _type: TypeControl; 
 
public get name(): string{ 
    let result = ""; 
    switch (this._type){ 
        case TypeControl.input: 
            result = "Ввод текста"; 
            break; 
        case TypeControl.Select: 
            result = "Выбор значения из выпадающего списка" 
            break;     
    } 
    return result; 
} 
/**  
 *  
 * @param tc тип контроля  
*/ 
constructor(tc:TypeControl){ this._type = tc; } /** Получить информацию о контроле */ public abstract getInfo(): string; 
 
public abstract setValue(val: any); 
 
} 
 
class TextBox extends Control { public get options(): string[] { return ["prop1", "prop2"]; } protected value: number; /**Максимальная длина строки которую модно ввести в контрол */ private _maxlength: number; 
 
public get maxLength(): number { 
    return this._maxlength; 
} 
/**  
 *  
 * @param m Максимальная длина которую можно ввести в контрол 
*/ 
constructor(m: number) { 
    super(TypeControl.input); 
    this._maxlength = m; 
} 
/**Получить информацию о контроле*/ 
public getInfo(): string { 
    return control: name = ${this.name} | textBox: Максимальная длина строки = ${this._maxlength}; 
} 
 
public setValue(val: number): void { 
    this.value = val; 
} 
} 
 
class SelectBox extends Control { public get options(): string[] { return []; } protected value: string; 
 
private _items: Array<string>; 
 
constructor(items: Array<string> = []){ 
    super(TypeControl.Select); 
    this._items = items; 
} /**Получить информацию о контроле */ public getInfo(): string { /**Специальная функция редьюсер которая может проходиться по массиву и делать разные операции */ let str = this._items.reduce((d,c,array)=> { return d + ";" + c; }) return control: name = ${this.name} | SelectBox: Варианты для выбора = ${str}; } 
 
public setValue(val: string): void { 
    this.value = val; 
} 
} 
 
let textbox = new TextBox(10); console.log((textbox as Control).getInfo()); 
 
let selectbox = new SelectBox(["первый","второй","третий"]); console.log((selectbox as Control).getInfo());
