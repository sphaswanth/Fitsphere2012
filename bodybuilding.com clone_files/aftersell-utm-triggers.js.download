var l = Object.defineProperty;
var S = (o, t, e) => t in o ? l(o, t, { enumerable: !0, configurable: !0, writable: !0, value: e }) : o[t] = e;
var i = (o, t, e) => (S(o, typeof t != "symbol" ? t + "" : t, e), e);
class s {
  static get() {
    let t = null;
    try {
      t = JSON.parse(
        sessionStorage.getItem(this.SESSION_STORAGE_KEY) || "null"
      );
    } catch {
    }
    return t;
  }
  static set(t) {
    try {
      sessionStorage.setItem(this.SESSION_STORAGE_KEY, JSON.stringify(t));
    } catch {
    }
  }
}
i(s, "SESSION_STORAGE_KEY", "as-customer-trigger-data");
function m({
  urlSearchParams: o,
  existingCustomerData: t
}) {
  const e = [
    "utm_source",
    "utm_medium",
    "utm_campaign",
    "utm_term",
    "utm_id",
    "utm_content"
  ];
  let n = !1;
  const r = {};
  for (const a of e) {
    const c = o.get(a) || (t == null ? void 0 : t[a]);
    c && (n = !0, r[a] = c);
  }
  return n ? r : null;
}
const g = "https://start.aftersell.app";
function u({ cookie: o, cookieName: t }) {
  const e = new RegExp(`^${t}=`), n = o.split(";").map((a) => a.trim()).find((a) => e.test(a));
  return n ? n.replace(`${t}=`, "") : null;
}
function f({
  cookieName: o,
  onChange: t,
  callbackOnInitialValue: e
}) {
  let r = u({ cookie: document.cookie, cookieName: o });
  e && t(r), setInterval(() => {
    const a = u({ cookie: document.cookie, cookieName: o });
    a !== r && (r = a, t(a));
  }, 500);
}
f({
  cookieName: "cart",
  callbackOnInitialValue: !0,
  onChange: (o) => {
    const t = s.get(), e = m({
      urlSearchParams: new URLSearchParams(window.location.search),
      existingCustomerData: t
    });
    s.set(e), !(!o || !e) && fetch(`${g}/api/v1/storefrontSessions`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({ shop: window.Shopify.shop, cartToken: o, customerTriggerData: e })
    });
  }
});
