# Интерфейс YaPay

```typescript
/**
 * Хелперы.
 */

type Listener<T> = (event: T) => void;
type UnsubscribeCallback = () => void;

interface TypedObject<T> {
  type: T;
}


/**
 * Общие типы.
 */

/**
 * Должно быть больше 0 и не содержать больше двух знаков после запятой.
 * Например: 1.12, 5.1, 10.
 */
export type Price = string;

/**
 * Платежная криптограмма.
 */
export type PaymentToken = string;

/**
 * Окружение, в котором совершается платеж.
 */
export enum PaymentEnv {
  Production = 'PRODUCTION',
  Sandbox = 'SANDBOX'
}

/**
 * Код страны по стандарту ISO 3166-1 alpha-2.
 */
export enum CountryCode {
  Ru = 'RU',
  Us = 'US',
  By = 'BY'
}

/**
 * Код валюты по стандарту ISO 4217.
 */
export enum CurrencyCode {
  Rub = 'RUB',
  Byn = 'BYN',
  Usd = 'USD',
  Eur = 'EUR'
}


/**
 * Информация о продавце.
 */

export interface Merchant {
  /**
   * ID продавца.
   */
  id: string;

  /**
   * Имя продавца (отображается на платежной форме).
   */
  name: string;

  /**
   * URL продавца (необязательное поле).
   */
  url?: string;
}


/**
 * Информация о заказе.
 */

export interface OrderTotal {
  /**
   * Текст для поля total.
   */
  label?: string;
  amount: Price;
}

export interface OrderItem {
  label: string;
  amount: Price;
}

export interface Order {
  /**
   * ID заказа на стороне продавца.
   */
  id: string;
  total: OrderTotal;
  items?: OrderItem[];
}


/**
 * Описание методов оплаты.
 */

export enum PaymentMethodType {
  Card = 'CARD'
}

export enum AllowedAuthMethod {
  CloudToken = 'CLOUD_TOKEN',
  PanOnly = 'PAN_ONLY'
}

export enum AllowedCardNetwork {
  AmericanExpress = 'AMEX',
  Discover = 'DISCOVER',
  Jcb = 'JCB',
  Mastercard = 'MASTERCARD',
  Visa = 'VISA',
  VisaElectron = 'VISAELECTRON',
  Maestro = 'MAESTRO',
  Mir = 'MIR',
  UnionPay = 'UNIONPAY',
  Uzcard = 'UZCARD',
}

export interface CardPaymentMethod extends TypedObject<PaymentMethodType.Card> {
  /**
   * ID поставщика платежных услуг.
   */
  gateway: string;

  /**
   * ID магазина в системе поставщика платежных услуг.
   */
  gatewayMerchantId: string;

  /**
   * Платежные методы, которые поддерживает поставщик платежных услуг.
   */
  allowedAuthMethods: AllowedAuthMethod[];

  /**
   * Платежные системы, которые поддерживает сайт и поставщик платежных услуг.
   */
  allowedCardNetworks: AllowedCardNetwork[];
}

export type PaymentMethod =
  | CardPaymentMethod;

export interface CardPaymentMethodInfo extends TypedObject<PaymentMethodType.Card> {
  /**
   * Дополнительные данные о методе.
   */
  cardLast4: string;
  cardNetwork: string;
}

export type PaymentMethodInfo =
  | CardPaymentMethodInfo;

/**
 * Запрашиваемые контактные данные плательщика.
 */
export interface RequiredBillingContactFields {
  email?: boolean;
}

/**
 * Запрашиваемые данные с платежной формы.
 */
export interface RequiredFields {
  billingContact?: RequiredBillingContactFields;
}

/**
 * Возвращаемые данные плательщика.
 */
export interface BillingContactField {
  // Поле появится, если было запрошено в RequiredBillingContactFields.
  email?: string;
}

/**
 * Настройки для платежа.
 */

export interface PaymentSheet {
  /**
   * Версия клиентского SDK.
   */
  version: number;

  /**
   * countryCode необходим для продавцов из Европейской экономической зоны.
   */
  countryCode: CountryCode;
  currencyCode: CurrencyCode;
  merchant: Merchant;
  order: Order;
  paymentMethods: PaymentMethod[];
  requiredFields?: RequiredFields;
}

export interface PaymentData extends PaymentSheet {
  /**
   * @default PaymentEnv.PRODUCTION
   */
  env?: PaymentEnv;
}

export interface UpdatePaymentData {
  order?: Order;
}


/**
 * События формы.
 */

export enum PaymentEventType {
  Ready = 'ready',
  Abort = 'abort',
  Error = 'error',
  Process = 'process',
}

export type ReadyEvent = TypedObject<PaymentEventType.Ready>

export enum AbortEventReason {
  /**
   * Покупатель закрыл форму оплаты.
   */
  Close = 'CLOSE',

  /**
   * Покупатель не успел совершить оплату.
   */
  Timeout = 'TIMEOUT'
}

export interface AbortEvent extends TypedObject<PaymentEventType.Abort> {
  reason?: AbortEventReason;
}

export interface ErrorEvent extends TypedObject<PaymentEventType.Error> {
  reason?: string;
  details?: any;
}

export interface ProcessEvent extends TypedObject<PaymentEventType.Process> {
  token: PaymentToken;
  paymentMethodInfo: PaymentMethodInfo;
  // Поле появится, если было запрошено в PaymentSheet.
  billingContact?: BillingContactField;
}

export type PaymentEvent =
  | ReadyEvent
  | AbortEvent
  | ErrorEvent
  | ProcessEvent;


/**
 * Сообщения SDK.
 */

export enum MessageType {
  Payment = 'payment',
  Complete = 'complete',
}

export interface PaymentMessage extends TypedObject<MessageType.Payment> {
  sheet: PaymentSheet;
}

export enum CompleteReason {
  Success = 'success',
  Error = 'error',
  Close = 'close',
  AuthRedirect = 'auth-redirect',
}

export interface CompleteMessage extends TypedObject<MessageType.Complete> {
  reason: CompleteReason;
  errors?: any;
}

export type Message =
  | PaymentMessage
  | CompleteMessage;


/**
 * Настройки платежной кнопки.
 */

export type ButtonParent = HTMLElement | ShadowRoot;

export enum ButtonType {
  Simple = 'SIMPLE',
  Pay = 'PAY'
}

export enum ButtonTheme {
  White = 'WHITE',
  WhiteOutlined = 'WHITE-OUTLINED',
  Black = 'BLACK'
}

export enum ButtonWidth {
  Auto = 'AUTO',
  Max = 'MAX'
}

export interface ButtonOptions {
  /**
   * @default ButtonType.SIMPLE
   */
  type?: ButtonType;

  /**
   * @default ButtonTheme.RED
   */
  theme?: ButtonTheme;

  /**
   * @default ButtonWidth.AUTO
   */
  width?: ButtonWidth;
}


/**
 * События платежной кнопки.
 */

export enum ButtonEventType {
  Click = 'CLICK'
}


/**
 * Конструктор платежной кнопки.
 */

export declare class Button {
  constructor(options: ButtonOptions);

  static create(options: ButtonOptions): Button;

  /**
   * Добавить кнопку в DOM-дерева.
   */
  mount(parent: ButtonParent): void;

  /**
   * Удалить кнопку из DOM-дерева.
   */
  unmount(): void;

  /**
   * Удаляет все слушатели с кнопки и кнопку из DOM-дерева.
   */
  destroy(): void;

  /**
   * Слушатель на клик.
   * Используйте этот параметр для запуска процесса оплаты на клик по кнопке.
   */
  on(type: ButtonEventType.Click, listener: Listener<MouseEvent>): void;
}

/**
 * Платеж.
 */

export interface Payment {
  /**
   * Создает привязанный к платежу экземпляр кнопки.
   */
  createButton(options: ButtonOptions): Button;

  /**
   * Обновляет данные платежа.
   */
  update(updateData: UpdatePaymentData): void;

  /**
   * Запускает процесс оплаты.
   */
  checkout(): void;

  /**
   * Удаляет платеж.
   */
  destroy(): void;


  /**
   * Подписывает на события формы платежа.
   */

  /**
   * Форма оплаты загружена.
   */
  on(type: PaymentEventType.Ready, listener: Listener<ReadyEvent>): UnsubscribeCallback;

  /**
   * Оплата была отменена. Пример: пользователь закрыл форму.
   */
  on(type: PaymentEventType.Abort, listener: Listener<AbortEvent>): UnsubscribeCallback;

  /**
   * Произошла ошибка во время оплаты.
   */
  on(type: PaymentEventType.Error, listener: Listener<ErrorEvent>): UnsubscribeCallback;

  /**
   * Запустился процесс оплаты.
   * Вместе с событием возвращается платежный токен.
   */
  on(type: PaymentEventType.Process, listener: Listener<ProcessEvent>): UnsubscribeCallback;


  /**
   * Дополнительное управление состоянием формы оплаты.
   */

  /**
   * Сообщить форме об успешной оплате.
   */
  complete(reason: CompleteReason.Success): void;

  /**
   * Сообщить форме об ошибке оплаты.
   */
  complete(reason: CompleteReason.Error, errors: unknown): void;

  /**
   * Закрыть платежную форму.
   */
  complete(reason: CompleteReason.Close): void;

  /**
   * Сообщить форме о редиректе покупателя на стороннюю форму оплаты.
   */
  complete(reason: CompleteReason.AuthRedirect): void;
}

export interface YaPay {
  /**
   * Enums.
   */

  /**
   * Общие типы.
   */
  PaymentEnv: PaymentEnv;
  CountryCode: CountryCode;
  CurrencyCode: CurrencyCode;

  /**
   * Описание методов оплаты.
   */
  PaymentMethodType: PaymentMethodType;
  AllowedAuthMethod: AllowedAuthMethod;
  AllowedCardNetwork: AllowedCardNetwork;

  /**
   * События формы.
   */
  PaymentEventType: PaymentEventType;
  AbortEventReason: AbortEventReason;
  ErrorEventReason: ErrorEventReason;

  /**
   * Сообщения SDK.
   */
  MessageType: MessageType;
  CompleteReason: CompleteReason;

  /**
   * Настройки платежной кнопки.
   */
  ButtonType: ButtonType;
  ButtonTheme: ButtonTheme;
  ButtonWidth: ButtonWidth;

  /**
   * События платежной кнопки.
   */
  ButtonEventType: ButtonEventType;
}

/**
 * Ошибка создания платежа.
 */
export interface PaymentError extends Error {}

/**
 * Фабрика, создающая платеж.
 */
export interface createPayment {
  /**
   * @reject PaymentError
   */
  (paymentData: PaymentData): Promise<Payment>;
}

/**
 * Метод, проверяющий доступность {{ product }} для оплаты
 */
export interface ReadyToPayCheckParams {
  merchantId: Merchant['id'];

  paymentMethods?: PaymentMethod[];
}

export interface readyToPayCheck {
  (params: ReadyToPayCheckParams): Promise<boolean>;
}
```
