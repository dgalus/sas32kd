SAS Library examples
--------------------

**Import library:**

.. code-block:: python

  from sas32kd import Sas32kd

|

**Connect to SAS audio router TCP/IP Server Module:**

.. code-block:: python

   sas = Sas32kd(ip="10.10.10.10", port=1270, timeout=5)

Port and timeout are optional arguments.

|


**Disconnecting from TCP/IP Server Module:**

.. code-block:: python

   sas.disconnect()

|

**Take command:**
*take(input: int, output: int)*

.. code-block:: python

   res = sas.take(10, 300)

- inp: Input channel number
- outp: Output channel number

| returns: *Reply.OK* or *Reply.ERROR*
|

**Enhanced take command:**
*enhanced_take(inp: int, outp: int, gain: int, options: EnhancedTakeOptions)*

.. code-block:: python

   res = sas.enhanced_take(
     10,
     300,
     1500,
     EnhancedTakeOptions(
       PriorityLevel.STANDARD,
       ControlOptions.ON,
       ActionOptions.SUM,
       SuppliedGainValueUsage.YES,
       CurrentXpointTransitionCtlSpec.YES
     )
   )

- inp: Input channel number.
- outp: Output channel number.
- gain: Source target gain level (1/10 dB steps, 1024 = Unity; valid 0 to 2048).
- options: Options. (Refer: EnhancedTakeOptions class).

| returns: *Reply.OK* or *Reply.ERROR*
|

**Relay command:**
*relay(action: RelayAction, num: int)*

.. code-block:: python

   res = sas.relay(RelayAction.LATCH, 123)

- action: Action to be performed on relay. (Refer: RelayAction class).
- num: Relay number.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Opto command:**
*opto(action: OptoAction, num: int)*

.. code-block:: python

   res = sas.opto(OptoAction.ON, 123)

- action: Action to be performed on opto. (Refer: OptoAction class).
- num: Opto number.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Salvo command:**
*salvo(option: SalvoOption, num: int)*

.. code-block:: python

   res = sas.salvo(SalvoOption.ACTUAL_SALVO_NUM, 10)

- option: Ordering type of salvos. (Refer: SalvoOption class).
- num: Salvo number.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Crosspoint transition control:**
*crosspoint_transition_control(setting: CrosspointTransitionControlSetting, fade_in_time: FadeTime, fade_out_time: FadeTime, channel: int)*

.. code-block:: python

   res = sas.crosspoint_transition_control(
     CrosspointTransitionControlSetting.FADE_OUT_FADE_IN,
     FadeTime.T_5S,
     FadeTime.T_5S,
     30
   )

- setting: Type of transition. (Refer: CrosspointTransitionControlSetting class).
- fade_in_time: Fade in time. (Refer: FadeTime class).
- fade_out_time: Fade out time. (Refer: FadeTime class).
- channel: Output channel number.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Gain change command:**
*gain_change(inp: int, outp: int, gain: int, fade_time: FadeTime, stage: GainChangeStage)*

.. code-block:: python

   res = sas.gain_change(
     123,
     234,
     1500,
     FadeTime.T_3S,
     GainChangeStage.OUTPUT_GAIN_TRIM
   )

- inp: Input channel number.
- outp: Output channel number.
- gain: Source target gain level (1/10 dB steps, 1024 = Unity; valid 0 to 2048).
- fade_time: Fade time. (Refer: FadeTime class).
- stage: Gain change stage. (Refer: GainChangeStage class).

| returns: *Reply.OK* or *Reply.ERROR*
|

**Stereo link modifier:**
*stereo_link(option: StereoLinkOption, setting: StereoLinkSetting, channel: int)*

.. code-block:: python

   res = sas.stereo_link(
     StereoLinkOption.INPUT_LINK,
     StereoLinkSetting.LR_MONO_SUM,
     234
   )

- option: Input or output link. (Refer: StereoLinkOption class).
- setting: Mono, stereo, source dependent or LR mono sum. (Refer: StereoLinkSetting class).
- channel: Output channel number.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Console module control command:**
*console_module_control(action: ConsoleModuleAction, console_id: int, source: int)*

.. code-block:: python

   res = sas.console_module_control(
     ConsoleModuleAction.TURN_MODULE_ON_WITH_SOURCE_SELECTED,
     2,
     234
   )

- action: Console source/module control options. (Refer: ConsoleModuleAction class).
- console_id: System console number (1 to 256 or 999 = any).
- source: Source channel number (1 to 9998).

| returns: *Reply.OK* or *Reply.ERROR*
|

**Console module channel label override command:**
*console_module_channel_label_override(self, console_id: int, source: int, label: str)*

.. code-block:: python

   res = sas.console_module_channel_label_override(
     2,
     3,
     "PGM X   "
   )

- console_id: System console number (1 to 256 or 999 = any).
- source: Source channel number (1 to 9998).
- label: 8 character alpha label to be displayed by the addressed modules.

| returns: *Reply.OK* or *Reply.ERROR*
|

**Inquiry command:**
*inquiry(outp: int)*

.. code-block:: python

   res = sas.inquiry(123)

- outp: Output channel (1 to 256 or 999 - any).

| returns: Three digit input assigned to specified output or inputs assigned to each output in ascending order.
|

**Expanded channel inquiry command:**
*expanded_channel_inquiry(destination: int)*

.. code-block:: python

   res = sas.expanded_channel_inquiry(123)

- destination: Destination channel number (1 to 9998).

| returns: Dict with all sources currently assigned to output, with priority levels.
|

**Alphanumeric name inquiry command:**
*alphanumeric_name_inquiry(input_output: AlphanumericNameInquiryInputOutput, channel_num: int)*

.. code-block:: python

   res = sas.alphanumeric_name_inquiry(
     AlphanumericNameInquiryInputOutput.INPUT,
     123
   )

- input_output: Input or output. (Refer: AlphanumericNameInquiryInputOutput class).
- channel_num: Channel number. (1 to 256. 998 - all channel sorted alphabetically. 999 - all channels in order of channel number).

| returns: Alpha label for input or output.
|

**Feedback command:**
*feedback(replies: FeedbackReplies, feedback_tally: FeedbackTally, feedback_protocol: FeedbackProtocol)*

.. code-block:: python

  res = sas.feedback(
    FeedbackReplies.ENABLED,
    FeedbackTally.NUMERICAL_TALLY_AND_ALPHA_CHANGE_NOTIFICATION,
    FeedbackProtocol.THREE_DIGIT_ASCII_STYLE_XPOINT_TALLY
  )

- replies: Enable or disable replies. (Refer: FeedbackReplies class).
- feedback_tally: Feedback tally variants. (Refer: FeedbackTally class).
- feedback_protocol: Feedback protocol variants. (Refer: FeedbackProtocol class).

| returns: *Reply.OK* or *Reply.ERROR*.
|
