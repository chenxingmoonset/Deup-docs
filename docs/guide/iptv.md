# IPTV

[https://raw.githubusercontent.com/deup-io/deup/master/iptv.js](https://raw.githubusercontent.com/deup-io/deup/master/iptv.js){target=_blank}

```javascript
/**
 * IPTV plugin for Deup
 *
 * @class IPTV
 * @extends {Deup}
 * @author ZiHang Gao
 */
class IPTV extends Deup {
  /**
   * Define the basic configuration of the IPTV plugin
   *
   * @type {{layout: string, name: string}}
   */
  config = {
    name: 'IPTV - CCTV Live',
    layout: 'poster',
  };

  /**
   * Channel list
   *
   * @private
   * @type {{name: string, type: string, path: string, poster: string, url: string}[]}
   * @memberof IPTV
   * @see https://github.com/fanmingming/live
   */
  _channels = [
    {
      name: 'CCTV-1 综合',
      poster: 'https://s2.loli.net/2023/08/30/VhHLMk98rm2gYvu.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv1',
    },
    {
      name: 'CCTV-2 财经',
      poster: 'https://s2.loli.net/2023/08/30/2YqziAxuJmWZgEl.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv2',
    },
    {
      name: 'CCTV-3 综艺',
      poster: 'https://s2.loli.net/2023/08/30/gyWSnKhzotF1O7r.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv3',
    },
    {
      name: 'CCTV-4 中文国际',
      poster: 'https://s2.loli.net/2023/08/30/kWI5xNPCBpdqnY6.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv4',
    },
    {
      name: 'CCTV-5 体育',
      poster: 'https://s2.loli.net/2023/08/30/I5MqfnkLduwKjaQ.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv5',
    },
    {
      name: 'CCTV-5+ 体育赛事',
      poster: 'https://s2.loli.net/2023/08/30/Q9jdSYAGy5kFNm3.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv5p',
    },
    {
      name: 'CCTV-6 电影',
      poster: 'https://s2.loli.net/2023/08/30/wX5bjlpy6ZquCVL.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv6',
    },
    {
      name: 'CCTV-7 国防军事',
      poster: 'https://s2.loli.net/2023/08/30/grtoQpCzY4E37BN.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv7',
    },
    {
      name: 'CCTV-8 电视剧',
      poster: 'https://s2.loli.net/2023/08/30/2iu4ADUBPOv6snW.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv8',
    },
    {
      name: 'CCTV-9 纪录',
      poster: 'https://s2.loli.net/2023/08/30/IH4fAMm78dPVBJE.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv9',
    },
    {
      name: 'CCTV-10 科教',
      poster: 'https://s2.loli.net/2023/08/30/AHaGdMOt3ZWVpgQ.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv10',
    },
    {
      name: 'CCTV-11 戏曲',
      poster: 'https://s2.loli.net/2023/08/30/a8XNDkfgPUvruO3.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv11',
    },
    {
      name: 'CCTV-12 社会与法',
      poster: 'https://s2.loli.net/2023/08/30/adFC3INOh9mAw1X.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv12',
    },
    {
      name: 'CCTV-13 新闻',
      poster: 'https://s2.loli.net/2023/08/30/FKgm5LoV4hESc2J.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv13',
    },
    {
      name: 'CCTV-14 少儿',
      poster: 'https://s2.loli.net/2023/08/30/ThYMDHq9S5L1JNP.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv14',
    },
    {
      name: 'CCTV-15 音乐',
      poster: 'https://s2.loli.net/2023/08/30/HIrOpoen2D3zlda.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv15',
    },
    {
      name: 'CCTV-16 奥林匹克',
      poster: 'https://s2.loli.net/2023/08/30/U2B4aXSHverE6do.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv16',
    },
    {
      name: 'CCTV-17 农业农村',
      poster: 'https://s2.loli.net/2023/08/30/UefnGBCLMJXt3hQ.png',
      url: 'https://cntv.sbs/tv?auth=230830&id=cctv17',
    },
  ].map((channel) => ({
    ...channel,
    ...{ isLive: true, type: 'video', path: '' },
  }));

  check = () => true;
  get = (name) => _.find(this._channels, (channel) => channel.name === name);
  list = (path, offset, limit) => (offset === 0 ? this._channels : []);
  search = (path, keyword, offset, limit) =>
    offset === 0
      ? _.filter(this._channels, (channel) => channel.name.includes(keyword))
      : [];
}

Deup.execute(new IPTV());
```
